# Tarefa — Migração Flyway: tabela `mercado` · API
> Sprint 1 (06/07–20/07/2026) · Bloco: Cadastros · Item: Mercado · Passo 1/6 · Depende: base do projeto

## O que fazer
Criar a migração Flyway **V7** que cria a tabela `mercado` e espelhar os scripts no repo `contas-domesticas-db`.

## Passo a passo
1. Criar `src/main/resources/db/migration/V7__cria_tabela_mercado.sql`.
2. Colunas: id `bigint generated always as identity` + nome, tipo (SUPERMERCADO/CONSTRUCAO/FARMACIA/OUTRO), endereco, bairro, ativo + auditoria (`criado_em`, `criado_por`, `atualizado_em`, `atualizado_por`).
3. Adicionar PK (`pk_mercado`) e índices/único necessários.
4. Espelhar em `contas-domesticas-db/ddl/{tables,primary,index}/mercado.sql`.

## Onde mexer
- `contas-domesticas-api/src/main/resources/db/migration/V7__cria_tabela_mercado.sql`
- `contas-domesticas-db/ddl/{tables,primary,index}/mercado.sql`

## Critério de pronto (DoD)
- [ ] App sobe em `dev` e o Flyway aplica V7 sem erro
- [ ] Scripts espelhados no repo db

## Como testar
Subir no profile `dev` (Flyway aplica) ou rodar o teste de contexto; conferir tipos/constraints.
