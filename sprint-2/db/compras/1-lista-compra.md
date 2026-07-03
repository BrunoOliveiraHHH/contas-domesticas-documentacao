# Tarefa — Tabela `lista_compra` (DDL) · DB
> Sprint 2 (21/07–04/08/2026) · Bloco: Compras · Item: lista_compra · Depende: espelha Flyway V15 da API

## O que fazer
Criar os scripts DDL separados de `lista_compra`, espelho da migração Flyway **V15** da API.

## Passo a passo
1. `ddl/tables/lista_compra.sql` — `create table lista_compra`: id `bigint generated always as identity` + nome, tipo, mercado_id, carteira_id, data, status, despesa_gerada_id + auditoria (`criado_em/por`, `atualizado_em/por`).
2. `ddl/primary/lista_compra.sql` — `pk_lista_compra`.
3. `ddl/foreign/lista_compra.sql` e `ddl/index/lista_compra.sql` — fks mercado/carteira; fk_lista_compra_despesa → lancamento(id); ix_lista_compra_status.
4. `dml/inserts/lista_compra.sql` — seed, se houver.

## Onde mexer
- `contas-domesticas-db/ddl/{tables,primary,foreign,index}/lista_compra.sql`

## Critério de pronto (DoD)
- [ ] Scripts refletem o Flyway V15 (tipos, nomes, constraints)
- [ ] Nomes `pk_`/`uk_`/`ix_`/`fk_` consistentes

## Como testar
Conferir contra a migração `V15` da API; rodar os scripts em banco limpo (ordem tables→primary→foreign→index→inserts).
