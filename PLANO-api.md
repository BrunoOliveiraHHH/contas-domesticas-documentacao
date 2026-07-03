# Plano de Desenvolvimento — API (`contas-domesticas-api`)

> Contas Domésticas · Backend Spring Boot 3.5.16 / Java 17 / PostgreSQL / Flyway
> Roadmap **completo e detalhado**, item a item (sem agrupar). A **ordem** segue a dependência
> técnica; cada item traz modelo, endpoints, regras, dependências, critérios de aceite e testes.

## Visão

API **local** (uso próprio, sem servidor/deploy) que centraliza **finanças familiar e individual**,
**compras**, **investimentos** e **parâmetros configuráveis**, e serve de ponto de **sincronização**
entre os celulares. Reaproveita a base já pronta: `BaseEntity` → `EntidadeAuditavel` (auditoria via
`@EnableJpaAuditing`/`AuditorAware`), `AuditoriaFilter` (log automático de cada requisição),
`GlobalExceptionHandler` (ProblemDetail RFC 7807), Flyway como fonte de verdade do schema, testes em
H2 (profile `test`). Segurança hoje é `permitAll` temporário até o JWT entrar.

### Convenções aplicadas a todos os itens
- **Pacote base:** `br.com.contasdomesticas.api`.
- **Camadas:** `domain` (entidade) · `repository` (Spring Data) · `dto` (record request/response) ·
  `mapper` (MapStruct) · `service` · `controller` (`/api/v1/...`) · `exception`.
- **Entidades de domínio** estendem `EntidadeAuditavel` (ganham `criado_em/por`, `atualizado_em/por`);
  tabelas de log/junção podem estender só `BaseEntity`.
- **Validação** com Bean Validation nos DTOs; erros no padrão **ProblemDetail**.
- **Migração Flyway** `V4+` para cada item que altera schema (espelhada no repo `db`).
- **Testes automatizados** obrigatórios por item (repository `@DataJpaTest`, service `Mockito`,
  controller `@SpringBootTest`+`MockMvc`), no padrão da tarefa Usuário + Auditoria.
- **Valores monetários:** `BigDecimal` (coluna `numeric(15,2)`); **datas de competência:** `LocalDate`;
  **instantes/auditoria:** `Instant` (`timestamptz`).
- **Escopo (familiar/individual):** derivado da **carteira** do lançamento (item 5).

---

## 1. Usuário + Auditoria  *(feito)*

- **O que é:** cadastro de usuários (login/nome/senha BCrypt + auditáveis) e log automático de cada
  requisição HTTP (usuário, método, endpoint, status, IP, data/hora).
- **Entregue:** `Usuario`, `Auditoria`, repositórios, `UsuarioController` (`/api/v1/usuarios`),
  `AuditoriaFilter`, `JpaAuditingConfig`, Flyway `V1/V2/V3` (seed admin/admin), 14 testes verdes.
- **Referência:** `documentacao/sprint-1/api/1-usuario-e-auditoria.md`.

## 2. Segurança — infraestrutura JWT

- **O que é:** montar a base de JWT próprio (jjwt já no pom) sem ainda fechar os endpoints.
- **Componentes:** `JwtService` (gerar/validar access e refresh, ler `subject`/`claims`),
  `JwtProperties` (secret, `access-expiration` 15m, `refresh-expiration` 7d — já no `application.yml`),
  `JwtAuthenticationFilter` (`OncePerRequestFilter`: extrai `Bearer`, valida, popula
  `SecurityContext`), `UserDetailsService` custom (carrega `Usuario` por login).
- **Regras:** algoritmo HS256 com o secret configurado; token inválido/expirado → 401 ProblemDetail;
  não vaza motivo detalhado.
- **Depende:** 1.
- **Aceite:** token gerado é validado e devolve o login nas claims; filtro popula o contexto quando o
  header é válido e ignora quando ausente.
- **Testes:** `JwtServiceTest` (round-trip gerar→validar, expiração, assinatura adulterada);
  `JwtAuthenticationFilterTest` (header válido/ausente/expirado).

## 3. Autenticação — Login

- **O que é:** endpoint que troca credenciais por tokens.
- **Endpoint:** `POST /api/v1/auth/login` `{ login, senha }` → `{ accessToken, refreshToken, tipo:
  "Bearer", expiraEm }`.
- **Regras:** valida senha com `BCryptPasswordEncoder.matches`; credencial inválida → **401** (mensagem
  genérica); registra a tentativa na auditoria.
- **Depende:** 2.
- **Aceite:** credenciais corretas retornam tokens; incorretas retornam 401 sem revelar se o login
  existe.
- **Testes:** `AuthControllerIntegrationTest.deveAutenticarComCredenciaisValidas` /
  `deveRejeitar401ComCredenciaisInvalidas`.

## 4. Autenticação — Refresh e Logout

- **O que é:** renovar o access token e encerrar sessão.
- **Endpoints:** `POST /api/v1/auth/refresh` `{ refreshToken }` → novo par;
  `POST /api/v1/auth/logout` (invalida o refresh atual).
- **Regras:** refresh stateless por padrão; opção de **denylist** de refresh (tabela `token_revogado`)
  para logout efetivo — decidir na análise (uso próprio pode dispensar).
- **Depende:** 3.
- **Aceite:** refresh válido gera novo access; refresh expirado/revogado → 401.
- **Testes:** `deveRenovarComRefreshValido`, `deveRejeitarRefreshExpirado`.

## 5. Proteção dos endpoints (troca do permitAll)

- **O que é:** substituir o `permitAll` temporário por autorização real.
- **Componentes:** `SecurityConfig` com `authorizeHttpRequests` — público: `/api/v1/auth/**`,
  `/actuator/health`, `/swagger-ui/**`, `/v3/api-docs/**`; **autenticado:** todo o resto. Registrar o
  `JwtAuthenticationFilter` antes do `UsernamePasswordAuthenticationFilter`.
- **Regras:** papéis simples (ex.: `ADMIN`, `USUARIO`) se necessário; `AuditorAware` passa a ler o
  login autenticado real (hoje já lê o `SecurityContext`).
- **Depende:** 2, 3.
- **Aceite:** requisição sem token a endpoint protegido → 401; com token válido → 200; auditoria grava
  o usuário autenticado (não "anonimo").
- **Testes:** ajustar os testes de integração existentes para autenticar; `deveBloquearSemToken`.

## 6. Carteira (CRUD)

- **O que é:** a unidade que separa **familiar × individual** e agrupa saldos; é um CRUD (o usuário
  cria/edita/remove).
- **Entidade `Carteira`** (extends `EntidadeAuditavel`): `nome`, `tipo` (`FAMILIAR`/`INDIVIDUAL`),
  `dono` (`Usuario`, nulo quando familiar), `saldoInicial` (BigDecimal), `moeda` (default `BRL`),
  `cor`/`icone` (opcional), `ativa` (boolean).
- **Endpoints:** `/api/v1/carteiras` (POST, GET lista, GET/{id}, PUT/{id}, DELETE/{id}).
- **Regras:** carteira `INDIVIDUAL` só é visível ao dono; `FAMILIAR` é compartilhada; não permitir
  remover carteira com lançamentos (bloqueia ou soft-delete `ativa=false`); saldo atual é derivado
  (saldo inicial ± lançamentos) — calculado, não persistido.
- **Depende:** 5.
- **Aceite:** CRUD completo; individual não aparece para outro usuário; remover carteira com movimento
  é impedido.
- **Testes:** repository (persistência + filtro por dono), service (regra de visibilidade e bloqueio de
  remoção), controller (CRUD + 404 + 409).

## 7. Categoria (CRUD, com subcategoria)

- **O que é:** classificação dos lançamentos, hierárquica.
- **Entidade `Categoria`** (extends `EntidadeAuditavel`): `nome`, `tipo`
  (`RECEITA`/`DESPESA`/`INVESTIMENTO`), `categoriaPai` (self-FK, nulo na raiz), `cor`/`icone`, `ativa`.
- **Endpoints:** `/api/v1/categorias` (CRUD) + filtro por `tipo`; `GET /api/v1/categorias/arvore`
  (raízes com subcategorias).
- **Regras:** subcategoria herda o `tipo` da pai; impedir ciclo (pai não pode ser descendente);
  categorias-semente sugeridas na análise (Moradia, Mercado, Salário, Renda fixa, etc.).
- **Depende:** 5.
- **Aceite:** CRUD + montagem da árvore; validação de tipo/ciclo.
- **Testes:** repository (árvore/filtro por tipo), service (herança de tipo, anti-ciclo), controller.

## 8. Forma de Pagamento (CRUD)

- **O que é:** meio usado no lançamento (dinheiro, PIX, débito, crédito...).
- **Entidade `FormaPagamento`** (extends `EntidadeAuditavel`): `nome`, `tipo`
  (`DINHEIRO`/`PIX`/`DEBITO`/`CREDITO`/`BOLETO`/`TRANSFERENCIA`), `carteiraVinculada` (opcional),
  `diaFechamento`/`diaVencimento` (só cartão de crédito), `ativa`.
- **Endpoints:** `/api/v1/formas-pagamento` (CRUD).
- **Regras:** para `CREDITO`, `diaFechamento`/`diaVencimento` viram base do parcelamento/fatura
  (item 12); para os demais, ignorados.
- **Depende:** 5 (e 6 se vincular carteira).
- **Aceite:** CRUD; validação condicional dos dias só para crédito.
- **Testes:** service (validação condicional), controller (CRUD).

## 9. Mercado / Fornecedor (CRUD)

- **O que é:** onde a compra é feita; base do histórico de preço.
- **Entidade `Mercado`** (extends `EntidadeAuditavel`): `nome`, `tipo`
  (`SUPERMERCADO`/`CONSTRUCAO`/`FARMACIA`/`OUTRO`), `endereco`/`bairro` (opcional), `ativo`.
- **Endpoints:** `/api/v1/mercados` (CRUD).
- **Depende:** 5.
- **Aceite:** CRUD completo.
- **Testes:** repository + controller (CRUD + 404).

## 10. Unidade de Medida (CRUD)

- **O que é:** unidade dos itens de compra (un, kg, g, L, mL, m).
- **Entidade `UnidadeMedida`** (extends `EntidadeAuditavel`): `nome`, `sigla`, `tipo`
  (`UNIDADE`/`PESO`/`VOLUME`/`COMPRIMENTO`), `fatorParaBase` (ex.: g→kg = 0,001) para normalizar preço.
- **Endpoints:** `/api/v1/unidades-medida` (CRUD).
- **Regras:** `fatorParaBase` permite comparar preço por unidade base (usado no item 22 e na
  calculadora de preço/unidade do app).
- **Depende:** 5.
- **Aceite:** CRUD; conversão coerente dentro do mesmo `tipo`.
- **Testes:** service (conversão), controller (CRUD).

## 11. Parâmetros — Índices financeiros

- **O que é:** guardar Selic, CDI, IPCA (parametrizáveis) para calculadoras e projeções.
- **Entidade `Parametro`** (extends `EntidadeAuditavel`): `chave` (`SELIC`, `CDI`, `IPCA`), `valor`
  (BigDecimal, % a.a.), `vigenciaInicio` (LocalDate), `descricao`. (histórico por vigência)
- **Endpoints:** `/api/v1/parametros` (CRUD) + `GET /api/v1/parametros/{chave}/vigente`.
- **Regras:** sempre retorna o valor vigente na data; permitir manter histórico de alterações.
- **Depende:** 5.
- **Aceite:** CRUD + consulta do valor vigente por data.
- **Testes:** service (seleção por vigência), controller.

## 12. Parâmetros — Alíquotas de imposto

- **O que é:** tabela de IR regressivo e IOF (parametrizáveis) para a calculadora de imposto.
- **Modelo:** reutiliza `Parametro` com chaves (`IR_ATE_180`=22,5; `IR_181_360`=20; `IR_361_720`=17,5;
  `IR_ACIMA_720`=15; `IOF_TABELA`) **ou** entidade `FaixaImposto` (`tipo`, `diasDe`, `diasAte`,
  `aliquota`) — decidir na análise.
- **Endpoints:** `/api/v1/parametros/impostos` (CRUD/lista das faixas vigentes).
- **Regras:** faixas contíguas e sem sobreposição; alíquota em %.
- **Depende:** 11.
- **Aceite:** faixas configuráveis retornam a alíquota certa por prazo em dias.
- **Testes:** service (resolver faixa por dias), controller.

## 13. Preferências

- **O que é:** ajustes do app parametrizáveis (não financeiros).
- **Entidade `Preferencia`** (por usuário e/ou global): `chave` (`CARTEIRA_PADRAO`, `REGRA_RATEIO`,
  `INICIO_MES`, `MOEDA`, ...), `valor`, `usuario` (nulo = global).
- **Endpoints:** `/api/v1/preferencias` (GET/PUT por chave).
- **Depende:** 5, 6.
- **Aceite:** ler/gravar preferência global e por usuário; valor default quando ausente.
- **Testes:** service (fallback global), controller.

## 14. Lançamento — modelo base

- **O que é:** o núcleo compartilhado por **receita** e **despesa** (e base de relatórios/sync).
- **Entidade `Lancamento`** (extends `EntidadeAuditavel`): `tipo` (`RECEITA`/`DESPESA`), `descricao`,
  `valor` (BigDecimal), `dataCompetencia` (LocalDate), `carteira` (FK), `categoria` (FK),
  `formaPagamento` (FK, opcional), `observacao`, `anexoUrl` (opcional).
- **Repositório/consultas:** por carteira, por período (mês), por categoria, por tipo.
- **Regras:** escopo herdado da carteira; valor > 0; data obrigatória.
- **Depende:** 6, 7, 8.
- **Aceite:** persiste com FKs válidas; consultas por período/carteira/tipo funcionam.
- **Testes:** repository (consultas por período/tipo), service (validações).

## 15. Receita

- **O que é:** entradas (salário, extra, rendimento, reembolso).
- **Endpoints:** `/api/v1/receitas` (CRUD) — cria `Lancamento` com `tipo=RECEITA` (categoria de tipo
  `RECEITA`).
- **Regras:** categoria precisa ser de tipo `RECEITA`; soma no saldo da carteira.
- **Depende:** 14.
- **Aceite:** CRUD; recusa categoria de tipo incompatível; entra no saldo.
- **Testes:** service (validação de tipo de categoria), controller (CRUD + 400).

## 16. Despesa

- **O que é:** saídas, com controle de pagamento.
- **Endpoints:** `/api/v1/despesas` (CRUD) — `Lancamento` `tipo=DESPESA` + `dataVencimento`,
  `dataPagamento`, `status` (`PAGO`/`PENDENTE`/`ATRASADO`).
- **Regras:** `status` derivado (pendente sem pagamento; atrasado se venceu e não pago; pago com
  `dataPagamento`); subtrai do saldo quando paga.
- **Depende:** 14.
- **Aceite:** CRUD; status calculado corretamente por data; entra no saldo ao pagar.
- **Testes:** service (transição de status por data), controller (CRUD + marcar como pago).

## 17. Recorrência (contas fixas)

- **O que é:** gerar lançamentos que se repetem (aluguel, luz, assinatura).
- **Entidade `Recorrencia`** (extends `EntidadeAuditavel`): modelo do lançamento (`descricao`, `valor`,
  `tipo`, `carteira`, `categoria`, `formaPagamento`), `frequencia`
  (`MENSAL`/`SEMANAL`/`ANUAL`), `diaVencimento`, `dataInicio`, `dataFim` (opcional), `ativa`.
- **Geração:** `@Scheduled` (ou endpoint `POST /api/v1/recorrencias/{id}/gerar`) cria o `Lancamento`
  do período; idempotente (não duplica o mesmo mês).
- **Endpoints:** `/api/v1/recorrencias` (CRUD) + gerar.
- **Depende:** 15, 16.
- **Aceite:** gera 1 lançamento por período sem duplicar; respeita início/fim.
- **Testes:** service (geração idempotente por competência), controller.

## 18. Parcelamento / Fatura de cartão

- **O que é:** despesa dividida em N parcelas (compra no crédito).
- **Modelo:** `Lancamento` "pai" + `Parcela` (`numero`, `total`, `valorParcela`, `vencimento`,
  `status`) **ou** N lançamentos vinculados por `grupoParcela` (uuid). Vencimentos derivados do
  `diaFechamento`/`diaVencimento` da forma de pagamento (item 8).
- **Endpoints:** `POST /api/v1/despesas/parceladas` `{ valorTotal, parcelas, primeiroVencimento }`.
- **Regras:** soma das parcelas = total (ajuste do centavo na última); cada parcela tem seu status.
- **Depende:** 16, 8.
- **Aceite:** gera N parcelas com vencimentos corretos e soma exata.
- **Testes:** service (geração e arredondamento), controller.

## 19. Rateio — divisão da despesa familiar

- **O que é:** dividir uma despesa entre participantes e apurar quem deve a quem.
- **Entidades:** `Rateio` (`lancamento` FK, `tipo` `IGUAL`/`PROPORCIONAL`/`CUSTOM`) +
  `ParticipanteRateio` (`usuario`, `percentual` ou `valor`).
- **Endpoints:** `POST /api/v1/despesas/{id}/rateio`; `GET /api/v1/rateios/acerto?periodo=YYYY-MM`
  (saldo consolidado por usuário).
- **Regras:** soma dos percentuais = 100% (ou soma dos valores = total); `PROPORCIONAL` usa a renda
  (receitas do período) como peso.
- **Depende:** 16, 15 (proporcional).
- **Aceite:** rateio válido; acerto do mês retorna o líquido de cada um.
- **Testes:** service (igual/proporcional/custom + validação da soma), controller (acerto).

## 20. Compras — Produto (catálogo)

- **O que é:** um **catálogo reutilizável** de produtos; o item da lista referencia um produto (não
  texto livre), então preços/cotações se reaproveitam entre listas.
- **Entidade `Produto`** (extends `EntidadeAuditavel`): `nome`, `descricao`, `categoria` (opcional),
  `unidadeMedidaPadrao` (opcional), `codigoBarras` (opcional), `ativo`.
- **Endpoints:** `/api/v1/produtos` (CRUD) + busca por nome/categoria.
- **Depende:** 7, 10.
- **Aceite:** CRUD; produto reaproveitado em várias listas.

## 21. Compras — Lista

- **Entidade `ListaCompra`** (extends `EntidadeAuditavel`): `nome`, `tipo`
  (`MANTIMENTOS`/`CONSTRUCAO`), `carteira`, `data`, `status` (`ABERTA`/`FECHADA`/`ARQUIVADA`).
  O estabelecimento é escolhido **por item**. Listas **não fechadas permanecem no histórico**
  (reutilizáveis via duplicar). Fechar gera **1 despesa por estabelecimento** (vínculo 1-N).
- **Endpoints:** `/api/v1/listas-compra` (CRUD, filtro por status) + `/{id}/duplicar`.
- **Depende:** 6.

## 22. Compras — Item + Cotação de Produto (reutilizável)

- **Entidade `ItemCompra`** (extends `EntidadeAuditavel`): `listaCompra` (FK), `produto` (FK catálogo),
  `quantidade`, `unidadeMedida` (FK), `mercadoEscolhido` (FK), `precoUnitario` (snapshot da cotação
  escolhida), `comprado`.
- **Entidade `CotacaoProduto`** (extends `BaseEntity`): `produto` (FK), `mercado` (FK), `precoUnitario`,
  `data`, `origem` (`COTACAO`/`COMPRA`) — **várias por produto** (uma por estabelecimento, com
  histórico). É a cotação **reutilizável** e **substitui o antigo `PrecoHistorico`** (o preço realizado
  entra como `origem=COMPRA`).
- **Endpoints:** `/api/v1/produtos/{id}/cotacoes` (registrar/listar, ordenado por preço/unidade base);
  `PUT /api/v1/itens/{id}/escolha` (grava `mercadoEscolhido` + snapshot do preço).
- **Regras:** comparação normaliza pela unidade base (`fatorParaBase`); marcar comprado exige escolha.
- **Depende:** 20, 21, 9, 10.
- **Aceite:** cotações do produto reaproveitáveis; menor preço destacado; escolha grava o item.

## 23. Compras — Fechar lista → gera despesa por estabelecimento

- **O que é:** ao concluir a compra, **agrupar os itens pelo estabelecimento escolhido** e criar **uma
  despesa por estabelecimento**.
- **Endpoint:** `POST /api/v1/listas-compra/{id}/fechar` → para cada `mercadoEscolhido` cria um
  `Lancamento` (`DESPESA`, total do estabelecimento), marca `status=FECHADA`, vincula as despesas à
  lista (1-N) e grava no catálogo uma `CotacaoProduto` `origem=COMPRA` (preço realizado).
- **Regras:** idempotente (lista já fechada não gera novas despesas); item exige estabelecimento
  escolhido. Listas **não** fechadas ficam `ABERTA`/`ARQUIVADA` no histórico e podem ser **duplicadas**.
- **Depende:** 21, 22, 16.
- **Aceite:** fechar gera 1 despesa por estabelecimento; refechar não duplica.

## 24. Investimento — cadastro e aportes

- **O que é:** registrar investimentos e movimentações.
- **Entidades:** `Investimento` (extends `EntidadeAuditavel`): `nome`, `tipoInvestimento`
  (`RENDA_FIXA`/`RENDA_VARIAVEL`/`FUNDO`/`CRIPTO`/`PREVIDENCIA`/`POUPANCA`/`RESERVA_EMERGENCIA`),
  `instituicao`, `carteira`, `indexador` (`SELIC`/`CDI`/`IPCA`/`PRE`), `taxaContratada`,
  `dataAplicacao`, `dataVencimento` (opcional); `Aporte` (`investimento`, `valor`, `data`, `tipo`
  `APORTE`/`RESGATE`).
- **Endpoints:** `/api/v1/investimentos` (CRUD) + `/{id}/aportes` (CRUD).
- **Regras:** saldo aplicado = Σ aportes − Σ resgates; vincula à carteira (escopo).
- **Depende:** 6, 11.
- **Aceite:** CRUD de investimento e aportes; saldo aplicado correto.
- **Testes:** service (saldo aplicado), controller.

## 25. Investimento — posição e evolução patrimonial

- **O que é:** foto do patrimônio no tempo (saldo + rendimento).
- **Modelo:** `PosicaoInvestimento` (`investimento`, `data`, `saldoBruto`, `rendimentoAcumulado`) —
  snapshot manual ou calculado pelo indexador/parametro vigente.
- **Endpoints:** `GET /api/v1/investimentos/{id}/evolucao`;
  `GET /api/v1/investimentos/patrimonio?data=` (consolidado por carteira/escopo).
- **Regras:** rendimento estimado usa o índice vigente (item 11) quando não houver saldo informado.
- **Depende:** 24, 11.
- **Aceite:** evolução por investimento e patrimônio consolidado por data.
- **Testes:** service (consolidação + estimativa por índice), controller.

## 26. Suporte a calculadoras (parâmetros p/ o app)

- **O que é:** expor, num contrato estável, tudo que as calculadoras do app precisam (as calculadoras
  em si rodam no cliente).
- **Endpoint:** `GET /api/v1/calculadoras/parametros` → índices vigentes (Selic/CDI/IPCA) + faixas de
  IR/IOF (itens 11–12).
- **Depende:** 11, 12.
- **Aceite:** retorna todos os parâmetros vigentes num payload único.
- **Testes:** controller (payload completo e vigente).

## 27. Relatório — saldo do mês

- **O que é:** receita − despesa por período/carteira/escopo.
- **Endpoint:** `GET /api/v1/relatorios/saldo?periodo=YYYY-MM&carteira=&escopo=`.
- **Regras:** considera competência; separa realizado (pago) de previsto (pendente).
- **Depende:** 15, 16.
- **Aceite:** totais de receita, despesa e saldo corretos por filtro.
- **Testes:** service (agregação por período/escopo), controller.

## 28. Relatório — gasto por categoria

- **O que é:** distribuição das despesas por categoria/subcategoria.
- **Endpoint:** `GET /api/v1/relatorios/por-categoria?periodo=&tipo=`.
- **Regras:** agrega por categoria raiz e detalha subcategorias; percentual do total.
- **Depende:** 16, 7.
- **Aceite:** soma por categoria bate com o total do período.
- **Testes:** service (agrupamento hierárquico), controller.

## 29. Relatório — evolução patrimonial

- **O que é:** série temporal de patrimônio (saldos + investimentos).
- **Endpoint:** `GET /api/v1/relatorios/patrimonio?de=&ate=`.
- **Depende:** 25, 27.
- **Aceite:** série mensal consistente com posições e saldos.
- **Testes:** service (série temporal), controller.

## 30. Relatório — acerto de rateio

- **O que é:** consolidação do "quem deve a quem" no período (visão de relatório, além do item 19).
- **Endpoint:** `GET /api/v1/relatorios/rateio?periodo=YYYY-MM`.
- **Depende:** 19.
- **Aceite:** líquido por usuário e sugestão de acerto (mínimo de transferências).
- **Testes:** service (líquido + minimização), controller.

## 31. Sincronização — colunas e contrato

- **O que é:** preparar as tabelas sincronizáveis e o contrato de troca.
- **Schema:** adicionar `uuid` (identidade estável gerada no cliente), `versao` (long),
  `atualizado_em` (Instant) e `deletado` (boolean, soft-delete) às entidades sincronizáveis
  (lançamentos, carteiras, cadastros, compras, investimentos).
- **Endpoints:** `GET /api/v1/sync?desde=<instant>` (deltas por entidade) e
  `POST /api/v1/sync` (recebe mudanças do cliente).
- **Depende:** 6–25 (entidades a sincronizar).
- **Aceite:** delta retorna só o alterado desde o timestamp; upsert por `uuid`.
- **Testes:** service (delta por timestamp, upsert por uuid), controller.

## 32. Sincronização — resolução de conflito (merge)

- **O que é:** política de merge quando os dois lados alteram o mesmo registro.
- **Regra:** **last-write-wins** por `atualizado_em` (o mais recente vence); `deletado=true` funciona
  como tombstone; `versao` detecta conflito.
- **Depende:** 31.
- **Aceite:** conflito resolve pelo mais recente; deleção propaga; sem perda silenciosa.
- **Testes:** service (LWW, tombstone, versão divergente).

---

## Fora de escopo (uso local / futuro distante)
Multi-moeda real, Open Finance/integração bancária, notificações push server-side, deploy/servidor,
perfis de produção, multiusuário além de Bruno/Karla.
