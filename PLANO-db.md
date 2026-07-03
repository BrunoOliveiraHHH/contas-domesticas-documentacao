# Plano de Desenvolvimento — Banco (`contas-domesticas-db`)

> Contas Domésticas · Scripts SQL (PostgreSQL) — espelho organizado do Flyway da API
> Roadmap **completo e detalhado**, tabela a tabela (sem agrupar). A **ordem** segue a dependência
> técnica; cada item traz colunas, chaves/índices, FKs, notas e a migração Flyway correspondente.

## Visão

Repositório de **scripts SQL separados** que **espelham** as migrações Flyway da API (a fonte de
verdade). Só recebe item quem **persiste schema**: JWT é stateless e calculadoras/dashboard/testes não
geram tabela. Cada item aqui acompanha uma `V4+` na API.

### Convenções aplicadas a todos os itens
- **Estrutura de pastas:** `ddl/tables`, `ddl/primary`, `ddl/foreign`, `ddl/index`, `dml/inserts` —
  cada tabela distribui seus scripts nessas pastas.
- **Tipos:** PK `bigint generated always as identity`; dinheiro `numeric(15,2)`; percentuais
  `numeric(7,4)`; datas de competência `date`; instantes/auditoria `timestamptz`; textos `varchar(n)`;
  flags `boolean`.
- **Auditáveis** (espelho de `EntidadeAuditavel`): `criado_em timestamptz`, `criado_por varchar(100)`,
  `atualizado_em timestamptz`, `atualizado_por varchar(100)` nas tabelas de domínio.
- **Nomenclatura:** `pk_<tabela>`, `uk_<tabela>_<col>`, `ix_<tabela>_<col>`, `fk_<tabela>_<ref>`.
- **Seeds** idempotentes (`on conflict do nothing`).
- **Sincronização** (item 20): as tabelas sincronizáveis recebem `uuid`, `versao`, `atualizado_em`,
  `deletado`.

---

## 1. Usuário + Auditoria  *(feito)*

- **Tabelas:** `usuario` (login uk, nome_exibicao, senha, auditáveis) e `auditoria` (usuario,
  metodo_http, endpoint, status_resposta, endereco_ip, data_hora).
- **Chaves/índices:** `pk_usuario`, `uk_usuario_login`; `pk_auditoria`, `ix_auditoria_data_hora`,
  `ix_auditoria_usuario`.
- **Seed:** `dml/inserts/usuario_admin.sql` (admin/Admin, BCrypt, idempotente) — espelho do Flyway `V3`.
- **Referência:** `documentacao/sprint-1/db/1-usuario-e-auditoria.md`.

## 2. Carteira  *(V4)*

- **Tabela `carteira`:** `id`, `nome varchar(120)`, `tipo varchar(20)` (FAMILIAR/INDIVIDUAL),
  `dono_id bigint` (nulo se familiar), `saldo_inicial numeric(15,2) default 0`, `moeda varchar(3)
  default 'BRL'`, `cor varchar(20)`, `icone varchar(40)`, `ativa boolean default true`, auditáveis.
- **Chaves/índices:** `pk_carteira`; `fk_carteira_dono` → `usuario(id)`; `ix_carteira_dono`,
  `ix_carteira_tipo`.
- **Notas:** saldo atual é **derivado** (não persiste); `dono_id` obrigatório quando `tipo=INDIVIDUAL`
  (check/trigger opcional).
- **Depende:** 1.

## 3. Categoria  *(V5)*

- **Tabela `categoria`:** `id`, `nome varchar(120)`, `tipo varchar(20)`
  (RECEITA/DESPESA/INVESTIMENTO), `categoria_pai_id bigint` (self, nulo na raiz), `cor varchar(20)`,
  `icone varchar(40)`, `ativa boolean default true`, auditáveis.
- **Chaves/índices:** `pk_categoria`; `fk_categoria_pai` → `categoria(id)`; `ix_categoria_tipo`,
  `ix_categoria_pai`.
- **Notas:** subcategoria herda o `tipo` da pai (validado na API); evitar ciclos.
- **Depende:** 1.

## 4. Forma de Pagamento  *(V6)*

- **Tabela `forma_pagamento`:** `id`, `nome varchar(120)`, `tipo varchar(20)`
  (DINHEIRO/PIX/DEBITO/CREDITO/BOLETO/TRANSFERENCIA), `carteira_id bigint` (opcional),
  `dia_fechamento smallint` (só crédito), `dia_vencimento smallint` (só crédito), `ativa boolean
  default true`, auditáveis.
- **Chaves/índices:** `pk_forma_pagamento`; `fk_forma_pagamento_carteira` → `carteira(id)`.
- **Depende:** 2.

## 5. Mercado / Fornecedor  *(V7)*

- **Tabela `mercado`:** `id`, `nome varchar(150)`, `tipo varchar(20)`
  (SUPERMERCADO/ARMAZEM/MERCEARIA/CONSTRUCAO/FARMACIA/OUTRO), `endereco varchar(200)`, `bairro varchar(100)`,
  `ativo boolean default true`, auditáveis.
- **Chaves/índices:** `pk_mercado`; `ix_mercado_tipo`.
- **Depende:** 1.

## 6. Unidade de Medida  *(V8)*

- **Tabela `unidade_medida`:** `id`, `nome varchar(60)`, `sigla varchar(10)`, `tipo varchar(20)`
  (UNIDADE/PESO/VOLUME/COMPRIMENTO), `fator_para_base numeric(12,6) default 1`, auditáveis.
- **Chaves/índices:** `pk_unidade_medida`; `uk_unidade_medida_sigla`.
- **Notas:** `fator_para_base` normaliza preço por unidade base (comparação de preço).
- **Depende:** 1.

## 7. Parâmetro (índices + alíquotas)  *(V9)*

- **Tabela `parametro`:** `id`, `chave varchar(40)` (SELIC, CDI, IPCA, IR_ATE_180, IR_181_360,
  IR_361_720, IR_ACIMA_720, IOF...), `valor numeric(9,4)`, `vigencia_inicio date`, `descricao
  varchar(200)`, auditáveis.
- **Chaves/índices:** `pk_parametro`; `ix_parametro_chave_vigencia (chave, vigencia_inicio)`.
- **Alternativa (impostos):** tabela `faixa_imposto` (`tipo`, `dias_de`, `dias_ate`, `aliquota`) se
  preferir modelar faixas explícitas — decidir na análise.
- **Seed:** valores iniciais de Selic/CDI/IPCA e faixas de IR/IOF.
- **Depende:** 1.

## 8. Preferência  *(V10)*

- **Tabela `preferencia`:** `id`, `chave varchar(40)` (CARTEIRA_PADRAO, REGRA_RATEIO, INICIO_MES,
  MOEDA...), `valor varchar(120)`, `usuario_id bigint` (nulo = global), auditáveis.
- **Chaves/índices:** `pk_preferencia`; `fk_preferencia_usuario` → `usuario(id)`;
  `uk_preferencia_chave_usuario (chave, usuario_id)`.
- **Depende:** 1, 2.

## 9. Lançamento  *(V11)*

- **Tabela `lancamento`:** `id`, `tipo varchar(10)` (RECEITA/DESPESA), `descricao varchar(200)`,
  `valor numeric(15,2)`, `data_competencia date`, `data_vencimento date`, `data_pagamento date`,
  `status varchar(15)` (PAGO/PENDENTE/ATRASADO), `carteira_id`, `categoria_id`,
  `forma_pagamento_id`, `observacao varchar(300)`, `anexo_url varchar(300)`,
  `recorrencia_id bigint`, `grupo_parcela uuid`, auditáveis.
- **Chaves/índices:** `pk_lancamento`; `fk_lancamento_carteira/categoria/forma_pagamento/recorrencia`;
  `ix_lancamento_competencia`, `ix_lancamento_carteira`, `ix_lancamento_tipo_status`.
- **Notas:** receita e despesa compartilham a tabela via `tipo` (simplifica relatórios/sync);
  `status`/`data_pagamento` só fazem sentido em DESPESA.
- **Depende:** 2, 3, 4.

## 10. Recorrência  *(V12)*

- **Tabela `recorrencia`:** `id`, `descricao varchar(200)`, `valor numeric(15,2)`, `tipo varchar(10)`,
  `carteira_id`, `categoria_id`, `forma_pagamento_id`, `frequencia varchar(10)`
  (MENSAL/SEMANAL/ANUAL), `dia_vencimento smallint`, `data_inicio date`, `data_fim date`,
  `ativa boolean default true`, auditáveis.
- **Chaves/índices:** `pk_recorrencia`; FKs para carteira/categoria/forma_pagamento;
  `ix_recorrencia_ativa`.
- **Notas:** a geração cria `lancamento` com `recorrencia_id` preenchido (idempotência por
  competência via índice único opcional `uk_lancamento_recorrencia_competencia`).
- **Depende:** 9.

## 11. Parcela  *(V13)*

- **Tabela `parcela`:** `id`, `lancamento_id bigint` (pai) ou `grupo_parcela uuid`, `numero smallint`,
  `total smallint`, `valor_parcela numeric(15,2)`, `vencimento date`, `status varchar(15)`,
  auditáveis.
- **Chaves/índices:** `pk_parcela`; `fk_parcela_lancamento` → `lancamento(id)`;
  `ix_parcela_vencimento`.
- **Notas:** alternativamente, o parcelamento pode ser N `lancamento` ligados por `grupo_parcela` —
  então esta tabela é dispensada (decidir na análise).
- **Depende:** 9, 4.

## 12. Rateio  *(V14)*

- **Tabelas:** `rateio` (`id`, `lancamento_id`, `tipo varchar(15)` IGUAL/PROPORCIONAL/CUSTOM,
  auditáveis) e `participante_rateio` (`id`, `rateio_id`, `usuario_id`, `percentual numeric(7,4)`,
  `valor numeric(15,2)`).
- **Chaves/índices:** `pk_rateio`, `fk_rateio_lancamento` → `lancamento(id)`;
  `pk_participante_rateio`, `fk_participante_rateio_rateio` → `rateio(id)`,
  `fk_participante_rateio_usuario` → `usuario(id)`.
- **Notas:** soma dos percentuais = 100% (ou soma dos valores = total) validada na API.
- **Depende:** 9.

## 13. Produto (catálogo)  *(V15)*

- **Tabela `produto`:** `id`, `nome varchar(150)`, `descricao varchar(300)`, `categoria_id bigint`,
  `unidade_medida_padrao_id bigint`, `codigo_barras varchar(60)`, `ativo boolean default true`,
  auditáveis. **Catálogo reutilizável** entre listas.
- **Chaves/índices:** `pk_produto`; `fk_produto_categoria/unidade_medida_padrao`; `ix_produto_nome`.
- **Depende:** 3, 6.

## 14. Lista de Compra  *(V16)*

- **Tabela `lista_compra`:** `id`, `nome varchar(150)`, `tipo varchar(15)`
  (MANTIMENTOS/CONSTRUCAO), `carteira_id bigint`, `data date`,
  `status varchar(10)` (ABERTA/FECHADA/ARQUIVADA), auditáveis. Sem `mercado_id` (o estabelecimento é
  por item). Vínculo **1-N** com as despesas geradas: `lancamento.lista_compra_id` **ou** tabela de
  ligação `lista_compra_despesa` (decidir na análise).
- **Chaves/índices:** `pk_lista_compra`; `fk_lista_compra_carteira`; `ix_lista_compra_status`.
- **Notas:** listas não fechadas permanecem no histórico (reutilizáveis via duplicar).
- **Depende:** 2.

## 15. Item de Compra  *(V17)*

- **Tabela `item_compra`:** `id`, `lista_compra_id bigint`, `produto_id bigint` (catálogo),
  `quantidade numeric(12,3)`, `unidade_medida_id bigint`, `mercado_escolhido_id bigint`,
  `preco_unitario numeric(15,2)` (snapshot da cotação escolhida), `comprado boolean default false`,
  auditáveis.
- **Chaves/índices:** `pk_item_compra`; `fk_item_compra_lista` → `lista_compra(id)` (on delete
  cascade); `fk_item_compra_produto` → `produto(id)`; `fk_item_compra_unidade_medida`;
  `fk_item_compra_mercado_escolhido` → `mercado(id)`; `ix_item_compra_lista`.
- **Depende:** 13, 14, 6.

## 16. Cotação de Produto (reutilizável)  *(V18)*

- **Tabela `cotacao_produto`:** `id`, `produto_id bigint`, `mercado_id bigint`,
  `preco_unitario numeric(15,2)`, `data date`, `origem varchar(10)` (COTACAO/COMPRA), auditáveis.
  **Várias por produto** (uma por estabelecimento, com histórico) — base da comparação/escolha e do
  preço realizado no fechamento. **Substitui o antigo `preco_historico`.**
- **Chaves/índices:** `pk_cotacao_produto`; `fk_cotacao_produto` → `produto(id)`;
  `fk_cotacao_mercado` → `mercado(id)`; `ix_cotacao_produto_mercado`.
- **Depende:** 13, 5.

## 17. Investimento  *(V19)*

- **Tabela `investimento`:** `id`, `nome varchar(150)`, `tipo_investimento varchar(25)`
  (RENDA_FIXA/RENDA_VARIAVEL/FUNDO/CRIPTO/PREVIDENCIA/POUPANCA/RESERVA_EMERGENCIA),
  `instituicao varchar(120)`, `carteira_id bigint`, `indexador varchar(10)` (SELIC/CDI/IPCA/PRE),
  `taxa_contratada numeric(9,4)`, `data_aplicacao date`, `data_vencimento date`, auditáveis.
- **Chaves/índices:** `pk_investimento`; `fk_investimento_carteira` → `carteira(id)`;
  `ix_investimento_tipo`.
- **Depende:** 2.

## 18. Aporte  *(V20)*

- **Tabela `aporte`:** `id`, `investimento_id bigint`, `valor numeric(15,2)`, `data date`,
  `tipo varchar(10)` (APORTE/RESGATE), auditáveis.
- **Chaves/índices:** `pk_aporte`; `fk_aporte_investimento` → `investimento(id)` (on delete cascade);
  `ix_aporte_investimento_data`.
- **Notas:** saldo aplicado = Σ APORTE − Σ RESGATE (calculado na API).
- **Depende:** 17.

## 19. Posição de Investimento  *(V21)*

- **Tabela `posicao_investimento`:** `id`, `investimento_id bigint`, `data date`,
  `saldo_bruto numeric(15,2)`, `rendimento_acumulado numeric(15,2)`.
- **Chaves/índices:** `pk_posicao_investimento`; `fk_posicao_investimento` → `investimento(id)`;
  `uk_posicao_investimento_data (investimento_id, data)`.
- **Notas:** snapshot manual ou calculado pelo indexador/parametro vigente; base da evolução
  patrimonial.
- **Depende:** 17, 7.

## 20. Preferência de rateio / dados auxiliares

- **O que é:** eventuais tabelas de apoio que surgirem (ex.: `regra_rateio` reutilizável). Manter como
  placeholder; criar só se a modelagem da API pedir.
- **Depende:** 12.

## 21. Colunas de Sincronização  *(V22)*

- **O que é:** habilitar o sync/merge em todas as tabelas de domínio sincronizáveis.
- **Alteração:** adicionar `uuid uuid` (identidade estável do cliente, `uk_<tabela>_uuid`),
  `versao bigint default 0`, `atualizado_em timestamptz`, `deletado boolean default false` em
  `carteira`, `categoria`, `forma_pagamento`, `mercado`, `unidade_medida`, `parametro`, `preferencia`,
  `lancamento`, `recorrencia`, `parcela`, `rateio`, `participante_rateio`, `produto`, `lista_compra`,
  `item_compra`, `cotacao_produto`, `investimento`, `aporte`, `posicao_investimento`.
- **Índices:** `ix_<tabela>_atualizado_em` para os deltas; `uk_<tabela>_uuid`.
- **Notas:** `deletado=true` funciona como tombstone; `versao` detecta conflito; merge é
  **last-write-wins** por `atualizado_em`.
- **Depende:** 2–19.

---

## Fora de escopo (por ora)
Particionamento, views/materialized views de relatório, triggers de negócio pesadas, jobs de banco —
otimizações futuras. Tabela de sessão/refresh só se o logout precisar de denylist (ver `PLANO-api.md`
item 4).
