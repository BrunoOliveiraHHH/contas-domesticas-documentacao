# Tarefa — Tabela `cotacao_item` (DDL) · DB
> Sprint 2 (21/07–04/08/2026) · Bloco: Compras · Item: cotacao_item · Depende: espelha Flyway V21 da API

## O que fazer
Criar os scripts DDL separados de `cotacao_item`, espelho da migração Flyway **V21** da API.

## Passo a passo
1. `ddl/tables/cotacao_item.sql`: id `bigint generated always as identity` + item_compra_id, mercado_id, preco_unitario numeric(15,2), data + auditoria.
2. `ddl/primary/cotacao_item.sql`: `pk_cotacao_item`.
3. `ddl/foreign/cotacao_item.sql` e `ddl/index/cotacao_item.sql`: fk_cotacao_item (on delete cascade) → item_compra(id); fk_cotacao_mercado → mercado(id); ix_cotacao_item.
4. `dml/inserts/cotacao_item.sql`: seed, se houver.

## Onde mexer
- `contas-domesticas-db/ddl/{tables,primary,foreign,index}/cotacao_item.sql`

## Critério de pronto (DoD)
- [ ] Scripts refletem o Flyway V21; nomes `pk_`/`uk_`/`ix_`/`fk_` consistentes

## Como testar
Conferir contra a migração V21; rodar em banco limpo.
