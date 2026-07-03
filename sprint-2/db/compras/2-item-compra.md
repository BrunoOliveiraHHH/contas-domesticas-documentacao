# Tarefa — Tabela `item_compra` (DDL) · DB
> Sprint 2 (21/07–04/08/2026) · Bloco: Compras · Item: item_compra · Depende: espelha Flyway V16 da API

## O que fazer
Criar os scripts DDL separados de `item_compra`, espelho da migração Flyway **V16** da API.

## Passo a passo
1. `ddl/tables/item_compra.sql`: id `bigint generated always as identity` + lista_compra_id, produto, categoria_id, quantidade numeric(12,3), unidade_medida_id, mercado_escolhido_id, preco_unitario numeric(15,2), comprado boolean + auditoria.
2. `ddl/primary/item_compra.sql`: `pk_item_compra`.
3. `ddl/foreign/item_compra.sql` e `ddl/index/item_compra.sql`: fk_item_compra_lista (on delete cascade); fks categoria/unidade; fk_item_compra_mercado_escolhido → mercado(id); ix_item_compra_lista.
4. `dml/inserts/item_compra.sql`: seed, se houver.

## Onde mexer
- `contas-domesticas-db/ddl/{tables,primary,foreign,index}/item_compra.sql`

## Critério de pronto (DoD)
- [ ] Scripts refletem o Flyway V16; nomes `pk_`/`uk_`/`ix_`/`fk_` consistentes

## Como testar
Conferir contra a migração V16; rodar em banco limpo.
