# Tarefa — Tabela `lista_compra` (DDL) · DB
> Sprint 2 (21/07–04/08/2026) · Bloco: Compras · Item: lista_compra · Depende: espelha Flyway V16 da API

## O que fazer
Criar os scripts DDL separados de `lista_compra`, espelho da migração Flyway **V16** da API.

## Passo a passo
1. `ddl/tables/lista_compra.sql`: id `bigint generated always as identity` + nome, tipo, carteira_id, data, status (ABERTA/FECHADA/ARQUIVADA) + auditoria.
2. `ddl/primary/lista_compra.sql`: `pk_lista_compra`.
3. `ddl/foreign/lista_compra.sql` e `ddl/index/lista_compra.sql`: fk carteira; ix_lista_compra_status; vínculo 1-N com despesas (lancamento.lista_compra_id ou tabela de ligação — decidir na análise).
4. `dml/inserts/lista_compra.sql`: seed, se houver.

## Onde mexer
- `contas-domesticas-db/ddl/{tables,primary,foreign,index}/lista_compra.sql`

## Critério de pronto (DoD)
- [ ] Scripts refletem o Flyway V16; nomes `pk_`/`uk_`/`ix_`/`fk_` consistentes

## Como testar
Conferir contra a migração V16; rodar em banco limpo.
