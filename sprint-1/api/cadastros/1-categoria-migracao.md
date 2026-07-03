# Tarefa — Migração Flyway: tabela `categoria` · API
> Sprint 1 (06/07–20/07/2026) · Bloco: Cadastros · Item: Categoria · Passo 1/6 · Depende: base do projeto

## O que fazer
Criar a migração Flyway **V5** que cria a tabela `categoria` e espelhar os scripts no repo `contas-domesticas-db`.

## Passo a passo
1. Criar `src/main/resources/db/migration/V5__cria_tabela_categoria.sql`.
2. Colunas: id `bigint generated always as identity` + nome, tipo (RECEITA/DESPESA/INVESTIMENTO), categoria_pai_id (self, nulo na raiz), cor, icone, ativa + auditoria (`criado_em`, `criado_por`, `atualizado_em`, `atualizado_por`).
3. Adicionar PK (`pk_categoria`) e índices/único necessários.
4. Espelhar em `contas-domesticas-db/ddl/{tables,primary,index}/categoria.sql`.

## Onde mexer
- `contas-domesticas-api/src/main/resources/db/migration/V5__cria_tabela_categoria.sql`
- `contas-domesticas-db/ddl/{tables,primary,index}/categoria.sql`

## Critério de pronto (DoD)
- [ ] App sobe em `dev` e o Flyway aplica V5 sem erro
- [ ] Scripts espelhados no repo db

## Como testar
Subir no profile `dev` (Flyway aplica) ou rodar o teste de contexto; conferir tipos/constraints.
