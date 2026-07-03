# Tarefa — Migração Flyway: tabela `parametro` · API
> Sprint 2 (21/07–04/08/2026) · Bloco: Parâmetros & Configuração · Item: Parametro · Passo 1/6 · Depende: base do projeto

## O que fazer
Criar a migração Flyway **V9** que cria a tabela `parametro` e espelhar os scripts no repo `contas-domesticas-db`.

## Passo a passo
1. Criar `src/main/resources/db/migration/V9__cria_tabela_parametro.sql`.
2. Colunas: id `bigint generated always as identity` + chave (SELIC/CDI/IPCA/...), valor numeric(9,4), vigencia_inicio date, descricao + auditoria (`criado_em`, `criado_por`, `atualizado_em`, `atualizado_por`).
3. Adicionar PK (`pk_parametro`) e índices/único necessários.
4. Espelhar em `contas-domesticas-db/ddl/{tables,primary,index}/parametro.sql`.

## Onde mexer
- `contas-domesticas-api/src/main/resources/db/migration/V9__cria_tabela_parametro.sql`
- `contas-domesticas-db/ddl/{tables,primary,index}/parametro.sql`

## Critério de pronto (DoD)
- [ ] App sobe em `dev` e o Flyway aplica V9 sem erro
- [ ] Scripts espelhados no repo db

## Como testar
Subir no profile `dev` (Flyway aplica) ou rodar o teste de contexto; conferir tipos/constraints.
