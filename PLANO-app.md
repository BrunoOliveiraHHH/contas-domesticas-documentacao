# Plano de Desenvolvimento — App (`contas-domesticas-app`)

> Contas Domésticas · Android Kotlin / Jetpack Compose / Room / Hilt / Retrofit
> Roadmap **completo e detalhado**, item a item (sem agrupar). A **ordem** segue a dependência
> técnica; cada item traz telas, dados locais (Room), integração, regras, dependências, aceite e
> verificação.

## Visão

App **offline-first** que espelha os dados no Room e **sincroniza** com a API. Reúne, num só produto,
**finanças familiar e individual** (via carteiras), **listas de compras** (mantimentos e material de
construção, por unidade/kg/volume, com histórico de preço), **investimentos**, **calculadoras** e uma
**tela de Configuração** parametrizável. Reaproveita a base pronta: Room (`Usuario`/`Auditoria`),
`AuditoriaInterceptor` (OkHttp grava cada chamada), Hilt, Retrofit + Moshi. A UI real em Compose ainda
será construída (hoje só a infra existe).

### Convenções aplicadas a todos os itens
- **Pacote base:** `br.com.contasdomesticas.app`; camadas `data/local` (Room: entity/dao), `data/remote`
  (Retrofit: api/dto/interceptor), `data/repository`, `di` (Hilt), `ui/<feature>` (screen + viewModel +
  state), `domain` (models/usecases quando fizer sentido).
- **Arquitetura:** MVVM + `StateFlow`/`UiState`; Compose com `Navigation-Compose`; injeção via Hilt.
- **Espelho Room** alinhado ao schema da API; timestamps `Long` (epoch millis); dinheiro em
  `Long`/centavos ou `BigDecimal` (definir e padronizar) para evitar erro de ponto flutuante.
- **Cada feature** = entidade Room + DAO + repositório + tela(s) Compose + ViewModel + integração
  Retrofit + registro no `AppDatabase` (nova `version` + migração) e no grafo Hilt.
- **Verificação** neste ambiente é **estática** (sem Gradle/SDK); aceite final é **build no Android
  Studio** e, onde indicado, **testes instrumentados** (item 37–39).
- **Calculadoras** são cálculo **client-side**; só consomem os parâmetros vindos da Configuração
  (que sincroniza com a API).

---

## 1. Usuário + Auditoria (local)  *(feito)*

- **O que é:** Room `UsuarioEntity`/`AuditoriaEntity` + DAOs + `AppDatabase` + `AuditoriaInterceptor`
  (grava cada chamada à API) + `NetworkModule`/`DatabaseModule` (Hilt) + `UsuarioApi`.
- **Referência:** `documentacao/sprint-1/app/1-usuario-e-auditoria.md`.

## 2. Fundação Compose — Navegação

- **O que é:** grafo de navegação central e host das telas.
- **Componentes:** `NavHost` + rotas tipadas (sealed `Screen`), `Scaffold` com `bottomBar`
  (Finanças, Compras, Investimentos, Relatórios, Config), deep-links internos.
- **Depende:** 1.
- **Aceite:** navegar entre destinos raiz e voltar corretamente; back-stack coerente.
- **Verificação:** estática + build; futuramente teste de navegação.

## 3. Fundação Compose — Tema / Design System

- **O que é:** identidade visual reutilizável.
- **Componentes:** `MaterialTheme` (cores claro/escuro, tipografia, shapes), tokens de espaçamento,
  ícones, formatação de moeda/data (pt-BR, `R$`, `America/Sao_Paulo`).
- **Depende:** 1.
- **Aceite:** tema claro/escuro aplicado; formatação monetária/datas consistente.

## 4. Fundação Compose — Componentes base

- **O que é:** biblioteca de componentes comuns.
- **Componentes:** campos (texto, moeda, data, dropdown), `ListItem`/cards, `EmptyState`,
  `LoadingState`, `ErrorState`, diálogos de confirmação, `CurrencyTextField`, `AmountText`.
- **Depende:** 3.
- **Aceite:** componentes reaproveitáveis parametrizáveis usados pelas features seguintes.

## 5. Login — Armazenamento de token

- **O que é:** guardar o token com segurança.
- **Componentes:** `TokenStore` sobre **DataStore + security-crypto** (access/refresh + expiração);
  `AuthInterceptor` (injeta `Authorization: Bearer` nas chamadas); `AuthAuthenticator` (renova no 401).
- **Depende:** api-3/4 (login/refresh), 1.
- **Aceite:** token persistido e injetado; renovação automática no 401; logout limpa o store.
- **Verificação:** estática + build; teste instrumentado do interceptor (item 38).

## 6. Login — Tela e fluxo

- **O que é:** autenticar o usuário.
- **Telas:** `LoginScreen` (login/senha, erro, loading) → chama `POST /auth/login` → guarda token →
  navega ao Dashboard; `Splash/AuthGate` decide login × home pelo token.
- **Depende:** 5, 2.
- **Aceite:** credenciais válidas entram; inválidas mostram erro; sessão persiste entre aberturas.

## 7. Sessão — Refresh, Logout e guarda de rota

- **O que é:** manter/encerrar sessão e proteger telas.
- **Componentes:** renovação via `AuthAuthenticator`; `logout` (limpa token e volta ao login);
  guarda nas rotas autenticadas.
- **Depende:** 5, 6.
- **Aceite:** refresh transparente; logout efetivo; rota protegida redireciona sem token.

## 8. Carteira — Room + Tela (CRUD)

- **O que é:** espelhar e gerenciar carteiras (familiar/individual).
- **Room:** `CarteiraEntity` (+ DAO) alinhada à API. **Telas:** lista + form (nome, tipo, dono, saldo
  inicial, cor/ícone). **Integração:** `CarteiraApi` (CRUD) + repositório.
- **Regras:** individual só do dono; seletor de carteira reutilizável nas outras telas.
- **Depende:** 7, api-6.
- **Aceite:** CRUD local + sync; seletor de carteira disponível.

## 9. Categoria — Room + Tela (CRUD, subcategoria)

- **O que é:** classificar lançamentos, com árvore.
- **Room:** `CategoriaEntity` (self-ref) + DAO. **Telas:** árvore + form (nome, tipo, pai, cor/ícone).
- **Depende:** 7, api-7.
- **Aceite:** CRUD + árvore; seletor de categoria filtrado por tipo.

## 10. Forma de Pagamento — Room + Tela (CRUD)

- **Room:** `FormaPagamentoEntity` + DAO. **Telas:** lista + form (tipo; dias só p/ crédito).
- **Depende:** 7, api-8.
- **Aceite:** CRUD; campos de crédito só aparecem para `CREDITO`.

## 11. Mercado — Room + Tela (CRUD)

- **Room:** `MercadoEntity` + DAO. **Telas:** lista + form.
- **Depende:** 7, api-9.
- **Aceite:** CRUD; seletor de mercado nas compras.

## 12. Unidade de Medida — Room + Tela (CRUD)

- **Room:** `UnidadeMedidaEntity` + DAO. **Telas:** lista + form (sigla, tipo, fator).
- **Depende:** 7, api-10.
- **Aceite:** CRUD; seletor de unidade nos itens de compra.

## 13. Configuração — Índices financeiros

- **O que é:** editar Selic/CDI/IPCA (parametrizáveis) usados pelas calculadoras.
- **Room:** `ParametroEntity` + DAO. **Telas:** seção "Índices" (valor + vigência).
- **Depende:** 7, api-11.
- **Aceite:** editar/consultar índices vigentes; sincroniza com a API.

## 14. Configuração — Alíquotas de imposto

- **O que é:** editar tabela IR regressivo e IOF.
- **Telas:** seção "Impostos" (faixas por prazo/alíquota).
- **Depende:** 13, api-12.
- **Aceite:** faixas configuráveis alimentam a calculadora de IR.

## 15. Configuração — Preferências

- **O que é:** carteira padrão, regra de rateio, início do mês, moeda.
- **Room/DataStore:** `PreferenciaEntity`/DataStore. **Telas:** seção "Preferências".
- **Depende:** 8, api-13.
- **Aceite:** preferências aplicadas como default nas telas de lançamento.

## 16. Configuração — Segurança / Biometria

- **O que é:** proteção de acesso do app.
- **Componentes:** troca de senha (chama API), **BiometricPrompt** para abrir o app, timeout de sessão.
- **Depende:** 7.
- **Aceite:** biometria opcional; troca de senha; auto-logout por inatividade.

## 17. Receita — Room + Telas

- **Room:** `LancamentoEntity` (tipo RECEITA) + DAO. **Telas:** lista + form (valor, data, carteira,
  categoria, forma pgto). **Integração:** `ReceitaApi`.
- **Depende:** 8, 9, 10, 15.
- **Aceite:** CRUD local + sync; entra no saldo/saldos exibidos.

## 18. Despesa — Room + Telas

- **Room:** `LancamentoEntity` (tipo DESPESA) + DAO. **Telas:** lista + form (+ vencimento, status,
  marcar como pago). **Integração:** `DespesaApi`.
- **Depende:** 8, 9, 10, 15.
- **Aceite:** CRUD; status pago/pendente/atrasado visível; ação "marcar pago".

## 19. Recorrência — UI

- **O que é:** cadastrar contas fixas e ver as geradas.
- **Telas:** form de recorrência (frequência, dia, início/fim) + lista de recorrências; disparo/consulta
  das geradas.
- **Depende:** 18, api-17.
- **Aceite:** recorrência criada gera lançamentos no período; sem duplicar.

## 20. Parcelamento — UI

- **O que é:** lançar despesa parcelada e acompanhar parcelas.
- **Telas:** form (valor total, nº parcelas, 1º vencimento) → lista das parcelas com status.
- **Depende:** 18, api-18.
- **Aceite:** N parcelas com vencimentos e soma corretos.

## 21. Rateio — UI e acerto

- **O que é:** dividir despesa entre pessoas e ver o acerto do mês.
- **Telas:** no form da despesa, seção "rateio" (igual/proporcional/custom); tela "Acerto do mês"
  (quem deve a quem).
- **Depende:** 18, api-19.
- **Aceite:** rateio válido (soma 100%); acerto do período correto.

## 22. Compras — Lista (Room + Tela)

- **Room:** `ListaCompraEntity` + DAO. **Telas:** lista de listas + form (nome, tipo, mercado,
  carteira). **Integração:** `ListaCompraApi`.
- **Depende:** 8, 11.
- **Aceite:** CRUD; totais estimado/real exibidos.

## 23. Compras — Item com unidade/preço

- **Room:** `ItemCompraEntity` + DAO. **Telas:** adicionar/editar item (produto, categoria, quantidade,
  unidade, preço estimado/real, comprado).
- **Regras:** total = qtd × preço; marcar comprado pede preço real.
- **Depende:** 22, 12, api-21.
- **Aceite:** itens com cálculo de total; marcar comprado atualiza total real.

## 24. Compras — Histórico de preço

- **O que é:** comparar onde o produto está mais barato.
- **Telas:** ao digitar o produto, mostra o menor preço/unidade e histórico por mercado.
- **Depende:** 23, api-22.
- **Aceite:** histórico e menor preço por unidade base exibidos.

## 25. Compras — Fechar lista → despesa

- **O que é:** concluir a compra gerando 1 despesa.
- **Telas:** ação "Fechar lista" → confirma total → cria despesa (via API) → mostra vínculo.
- **Depende:** 24, 18, api-23.
- **Aceite:** fechar gera 1 despesa com o total; lista marcada como fechada; não duplica.

## 26. Investimento — Room + Telas

- **Room:** `InvestimentoEntity` + `AporteEntity` + DAOs. **Telas:** lista + form (tipo, instituição,
  indexador, taxa, datas) + aportes/resgates.
- **Depende:** 8, 13, api-24.
- **Aceite:** CRUD de investimento e aportes; saldo aplicado correto.

## 27. Investimento — Evolução (gráfico)

- **O que é:** evolução patrimonial no tempo.
- **Telas:** gráfico de linha (saldo/rendimento) + consolidado por carteira.
- **Depende:** 26, api-25.
- **Aceite:** série coerente com aportes e índice vigente.

## 28. Calculadora — Investimento

- **O que é:** projeção de juros compostos com aportes.
- **Entradas:** valor inicial, aporte mensal, taxa (% a.a. ou % do CDI/Selic da Config), prazo.
- **Saídas:** valor futuro, total investido, rendimento bruto e **líquido** (aplica IR do item 29).
- **Depende:** 13 (índices).
- **Aceite:** resultado confere com cálculo manual de juros compostos; usa índice da Config.
- **Verificação:** teste unitário do cálculo (JVM) — não precisa de device.

## 29. Calculadora — IR sobre investimentos

- **O que é:** imposto no resgate de renda fixa.
- **Entradas:** valor aplicado, rendimento, dias aplicados.
- **Saídas:** alíquota IR regressiva (22,5%→15%) + **IOF** regressivo (primeiros 30 dias), imposto e
  valor líquido — faixas vindas da Config (item 14).
- **Depende:** 14.
- **Aceite:** alíquota correta por faixa de dias; IOF nos primeiros 30 dias; líquido exato.
- **Verificação:** teste unitário do cálculo.

## 30. Calculadora — Financiamento (Price/SAC)

- **O que é:** simular parcelas de empréstimo/financiamento.
- **Entradas:** valor, taxa a.m., prazo. **Saídas:** tabela **Price** (parcela fixa) e **SAC**
  (amortização constante), total de juros, custo total.
- **Depende:** 4 (componentes).
- **Aceite:** parcelas e juros conferem para Price e SAC.
- **Verificação:** teste unitário do cálculo.

## 31. Calculadora — Preço por unidade (compras)

- **O que é:** dizer qual opção compensa (por kg/L/un).
- **Entradas:** N opções (preço, quantidade, unidade). **Saídas:** preço por unidade base (via
  `fatorParaBase`) e a mais barata.
- **Depende:** 12, 24.
- **Aceite:** normaliza unidades e aponta a melhor opção.
- **Verificação:** teste unitário do cálculo.

## 32. Dashboard — Resumo do mês

- **O que é:** visão inicial (home).
- **Telas:** cards de receita, despesa e saldo do mês (por carteira/escopo), pendências a vencer.
- **Depende:** 17, 18, api-27.
- **Aceite:** números batem com os lançamentos do período.

## 33. Dashboard — Gastos por categoria

- **Telas:** gráfico (pizza/barras) de despesa por categoria + drill-down por subcategoria.
- **Depende:** 18, api-28.
- **Aceite:** soma por categoria = total do período.

## 34. Dashboard — Evolução patrimonial

- **Telas:** gráfico de patrimônio (saldos + investimentos) ao longo dos meses.
- **Depende:** 27, api-29.
- **Aceite:** série consistente com posições e saldos.

## 35. Sincronização — Worker

- **O que é:** sincronizar Room ↔ API em background.
- **Componentes:** `WorkManager` (sync periódico + on-demand), delta por `atualizado_em`, upsert por
  `uuid`, indicador de "última sincronização".
- **Depende:** 17–27, api-31.
- **Aceite:** dados criados num device aparecem no outro após sync.

## 36. Sincronização — Resolução de conflito + status UI

- **O que é:** aplicar merge e mostrar o estado.
- **Regra:** **mais recente vence** (por `atualizado_em`); soft-delete via tombstone; badge de
  pendências não sincronizadas.
- **Depende:** 35, api-32.
- **Aceite:** conflito resolve pelo mais recente; deleção propaga; UI mostra status.

## 37. Testes instrumentados — Room/DAO

- **O que é:** validar persistência local.
- **Escopo:** `@RunWith(AndroidJUnit4)` + Room in-memory; CRUD e queries dos DAOs (carteira, categoria,
  lançamento, compras, investimento).
- **Depende:** entidades correspondentes.
- **Aceite:** DAOs cobertos; migrações testadas.

## 38. Testes instrumentados — Interceptor e rede

- **Escopo:** `AuditoriaInterceptor` (grava no Room a cada chamada) e `AuthInterceptor` (injeta token,
  renova no 401) com `MockWebServer`.
- **Depende:** 5, 1.
- **Aceite:** cada chamada gera auditoria; token injetado; renovação no 401.

## 39. Testes instrumentados — Fluxos de UI

- **Escopo:** Compose UI tests dos fluxos-chave (login, criar despesa, fechar lista → despesa).
- **Depende:** telas correspondentes.
- **Aceite:** fluxos principais verdes no CI/instrumentado.

---

## Fora de escopo (por ora)
Widget de tela inicial, notificações push, Wear OS/tablet, exportação avançada (PDF/planilha),
temas customizados avançados, modo multiusuário além de Bruno/Karla.
