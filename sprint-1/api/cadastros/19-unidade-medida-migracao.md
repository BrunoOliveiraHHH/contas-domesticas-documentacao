# Tarefa — Migração Flyway: tabela `unidade_medida` · API
> Sprint 1 (06/07–20/07/2026) · Bloco: Cadastros · Item: UnidadeMedida · Passo 1/6 · Depende: base do projeto

## O que fazer
Criar a migração Flyway **V8** que cria a tabela `unidade_medida` e espelhar os scripts no repo `contas-domesticas-db`.

## Passo a passo
1. Criar `src/main/resources/db/migration/V8__cria_tabela_unidade_medida.sql`.
2. Colunas: id `bigint generated always as identity` + nome, sigla (única), tipo (UNIDADE/PESO/VOLUME/COMPRIMENTO), fator_para_base numeric(12,6) + auditoria (`criado_em`, `criado_por`, `atualizado_em`, `atualizado_por`).
3. Adicionar PK (`pk_unidade_medida`) e índices/único necessários.
4. Espelhar em `contas-domesticas-db/ddl/{tables,primary,index}/unidade_medida.sql`.

## Onde mexer
- `contas-domesticas-api/src/main/resources/db/migration/V8__cria_tabela_unidade_medida.sql`
- `contas-domesticas-db/ddl/{tables,primary,index}/unidade_medida.sql`

## Critério de pronto (DoD)
- [ ] App sobe em `dev` e o Flyway aplica V8 sem erro
- [ ] Scripts espelhados no repo db

## Como testar
Subir no profile `dev` (Flyway aplica) ou rodar o teste de contexto; conferir tipos/constraints.
