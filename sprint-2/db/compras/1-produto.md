# Tarefa — Tabela `produto` (DDL) · DB
> Sprint 2 (21/07–04/08/2026) · Bloco: Compras · Item: produto · Depende: espelha Flyway V15 da API

## O que fazer
Criar os scripts DDL separados de `produto`, espelho da migração Flyway **V15** da API.

## Passo a passo
1. `ddl/tables/produto.sql`: id `bigint generated always as identity` + nome, descricao, categoria_id, unidade_medida_padrao_id, codigo_barras, ativo boolean + auditoria.
2. `ddl/primary/produto.sql`: `pk_produto`.
3. `ddl/foreign/produto.sql` e `ddl/index/produto.sql`: fks categoria/unidade_medida_padrao; ix_produto_nome; catálogo reutilizável.
4. `dml/inserts/produto.sql`: seed, se houver.

## Onde mexer
- `contas-domesticas-db/ddl/{tables,primary,foreign,index}/produto.sql`

## Critério de pronto (DoD)
- [ ] Scripts refletem o Flyway V15; nomes `pk_`/`uk_`/`ix_`/`fk_` consistentes

## Como testar
Conferir contra a migração V15; rodar em banco limpo.
