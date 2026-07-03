# Tarefa — Migração Flyway: tabela `preferencia` · API
> Sprint 2 (21/07–04/08/2026) · Bloco: Parâmetros & Configuração · Item: Preferencia · Passo 1/6 · Depende: base do projeto

## O que fazer
Criar a migração Flyway **V10** que cria a tabela `preferencia` e espelhar os scripts no repo `contas-domesticas-db`.

## Passo a passo
1. Criar `src/main/resources/db/migration/V10__cria_tabela_preferencia.sql`.
2. Colunas: id `bigint generated always as identity` + chave (CARTEIRA_PADRAO/REGRA_RATEIO/INICIO_MES/MOEDA/...), valor, usuario_id (nulo=global) + auditoria (`criado_em`, `criado_por`, `atualizado_em`, `atualizado_por`).
3. Adicionar PK (`pk_preferencia`) e índices/único necessários.
4. Espelhar em `contas-domesticas-db/ddl/{tables,primary,index}/preferencia.sql`.

## Onde mexer
- `contas-domesticas-api/src/main/resources/db/migration/V10__cria_tabela_preferencia.sql`
- `contas-domesticas-db/ddl/{tables,primary,index}/preferencia.sql`

## Critério de pronto (DoD)
- [ ] App sobe em `dev` e o Flyway aplica V10 sem erro
- [ ] Scripts espelhados no repo db

## Como testar
Subir no profile `dev` (Flyway aplica) ou rodar o teste de contexto; conferir tipos/constraints.
