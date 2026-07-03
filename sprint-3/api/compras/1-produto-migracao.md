# Tarefa — Migração Flyway: tabela `produto` · API
> Sprint 3 (05/08–19/08/2026) · Bloco: Compras · Item: Produto · Passo 1/6 · Depende: base do projeto

## O que fazer
Criar a migração Flyway **V15** que cria a tabela `produto` e espelhar os scripts no repo `contas-domesticas-db`.

## Passo a passo
1. Criar `src/main/resources/db/migration/V15__cria_tabela_produto.sql`.
2. Colunas: id `bigint generated always as identity` + nome, descricao, categoria_id, unidade_medida_padrao_id, codigo_barras (opcional), ativo boolean + auditoria (`criado_em`, `criado_por`, `atualizado_em`, `atualizado_por`).
3. Adicionar PK (`pk_produto`) e índices/único necessários.
4. Espelhar em `contas-domesticas-db/ddl/{tables,primary,index}/produto.sql`.

## Onde mexer
- `contas-domesticas-api/src/main/resources/db/migration/V15__cria_tabela_produto.sql`
- `contas-domesticas-db/ddl/{tables,primary,index}/produto.sql`

## Critério de pronto (DoD)
- [ ] App sobe em `dev` e o Flyway aplica V15 sem erro
- [ ] Scripts espelhados no repo db

## Como testar
Subir no profile `dev` (Flyway aplica) ou rodar o teste de contexto; conferir tipos/constraints.
