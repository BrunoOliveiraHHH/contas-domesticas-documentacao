# Tarefa — Tabela `cotacao_produto` (DDL) · DB
> Sprint 2 (21/07–04/08/2026) · Bloco: Compras · Item: cotacao_produto · Depende: espelha Flyway V18 da API

## O que fazer
Criar os scripts DDL separados de `cotacao_produto`, espelho da migração Flyway **V18** da API.

## Passo a passo
1. `ddl/tables/cotacao_produto.sql`: id `bigint generated always as identity` + produto_id, mercado_id, preco_unitario numeric(15,2), data, origem (COTACAO/COMPRA) + auditoria.
2. `ddl/primary/cotacao_produto.sql`: `pk_cotacao_produto`.
3. `ddl/foreign/cotacao_produto.sql` e `ddl/index/cotacao_produto.sql`: fk_cotacao_produto → produto(id); fk_cotacao_mercado → mercado(id); ix_cotacao_produto_mercado; substitui o antigo preco_historico.
4. `dml/inserts/cotacao_produto.sql`: seed, se houver.

## Onde mexer
- `contas-domesticas-db/ddl/{tables,primary,foreign,index}/cotacao_produto.sql`

## Critério de pronto (DoD)
- [ ] Scripts refletem o Flyway V18; nomes `pk_`/`uk_`/`ix_`/`fk_` consistentes

## Como testar
Conferir contra a migração V18; rodar em banco limpo.
