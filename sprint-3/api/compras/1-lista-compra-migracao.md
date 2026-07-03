# Tarefa — Migração Flyway: tabela `lista_compra` · API
> Sprint 3 (05/08–19/08/2026) · Bloco: Compras · Item: ListaCompra · Passo 1/6 · Depende: base do projeto

## O que fazer
Criar a migração Flyway **V15** que cria a tabela `lista_compra` e espelhar os scripts no repo `contas-domesticas-db`.

## Passo a passo
1. Criar `src/main/resources/db/migration/V15__cria_tabela_lista_compra.sql`.
2. Colunas: id `bigint generated always as identity` + nome, tipo (MANTIMENTOS/CONSTRUCAO), carteira_id, data, status (ABERTA/FECHADA/ARQUIVADA) + auditoria (`criado_em`, `criado_por`, `atualizado_em`, `atualizado_por`).
3. Adicionar PK (`pk_lista_compra`) e índices/único necessários.
4. Espelhar em `contas-domesticas-db/ddl/{tables,primary,index}/lista_compra.sql`.

## Onde mexer
- `contas-domesticas-api/src/main/resources/db/migration/V15__cria_tabela_lista_compra.sql`
- `contas-domesticas-db/ddl/{tables,primary,index}/lista_compra.sql`

## Critério de pronto (DoD)
- [ ] App sobe em `dev` e o Flyway aplica V15 sem erro
- [ ] Scripts espelhados no repo db

## Como testar
Subir no profile `dev` (Flyway aplica) ou rodar o teste de contexto; conferir tipos/constraints.
