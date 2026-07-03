# Tarefa — Migração Flyway: tabela `investimento` · API
> Sprint 3 (05/08–19/08/2026) · Bloco: Investimentos · Item: Investimento · Passo 1/6 · Depende: base do projeto

## O que fazer
Criar a migração Flyway **V19** que cria a tabela `investimento` e espelhar os scripts no repo `contas-domesticas-db`.

## Passo a passo
1. Criar `src/main/resources/db/migration/V18__cria_tabela_investimento.sql`.
2. Colunas: id `bigint generated always as identity` + nome, tipo_investimento (RENDA_FIXA/RENDA_VARIAVEL/FUNDO/CRIPTO/PREVIDENCIA/POUPANCA/RESERVA_EMERGENCIA), instituicao, carteira_id, indexador (SELIC/CDI/IPCA/PRE), taxa_contratada, data_aplicacao, data_vencimento + auditoria (`criado_em`, `criado_por`, `atualizado_em`, `atualizado_por`).
3. Adicionar PK (`pk_investimento`) e índices/único necessários.
4. Espelhar em `contas-domesticas-db/ddl/{tables,primary,index}/investimento.sql`.

## Onde mexer
- `contas-domesticas-api/src/main/resources/db/migration/V18__cria_tabela_investimento.sql`
- `contas-domesticas-db/ddl/{tables,primary,index}/investimento.sql`

## Critério de pronto (DoD)
- [ ] App sobe em `dev` e o Flyway aplica V19 sem erro
- [ ] Scripts espelhados no repo db

## Como testar
Subir no profile `dev` (Flyway aplica) ou rodar o teste de contexto; conferir tipos/constraints.
