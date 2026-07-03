# Tarefa — Tabela `item_compra` (DDL) · DB
> Sprint 2 (21/07–04/08/2026) · Bloco: Compras · Item: item_compra · Depende: espelha Flyway V16 da API

## O que fazer
Criar os scripts DDL separados de `item_compra`, espelho da migração Flyway **V16** da API.

## Passo a passo
1. `ddl/tables/item_compra.sql` — `create table item_compra`: id `bigint generated always as identity` + lista_compra_id, produto, categoria_id, quantidade numeric(12,3), unidade_medida_id, preco_unitario_estimado, preco_unitario_real, comprado boolean, mercado_id + auditoria (`criado_em/por`, `atualizado_em/por`).
2. `ddl/primary/item_compra.sql` — `pk_item_compra`.
3. `ddl/foreign/item_compra.sql` e `ddl/index/item_compra.sql` — fk_item_compra_lista (on delete cascade); fks categoria/unidade/mercado; ix_item_compra_lista.
4. `dml/inserts/item_compra.sql` — seed, se houver.

## Onde mexer
- `contas-domesticas-db/ddl/{tables,primary,foreign,index}/item_compra.sql`

## Critério de pronto (DoD)
- [ ] Scripts refletem o Flyway V16 (tipos, nomes, constraints)
- [ ] Nomes `pk_`/`uk_`/`ix_`/`fk_` consistentes

## Como testar
Conferir contra a migração `V16` da API; rodar os scripts em banco limpo (ordem tables→primary→foreign→index→inserts).
