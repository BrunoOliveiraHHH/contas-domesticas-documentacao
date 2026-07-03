# Tarefa — Tabela `preco_historico` (DDL) · DB
> Sprint 2 (21/07–04/08/2026) · Bloco: Compras · Item: preco_historico · Depende: espelha Flyway V17 da API

## O que fazer
Criar os scripts DDL separados de `preco_historico`, espelho da migração Flyway **V17** da API.

## Passo a passo
1. `ddl/tables/preco_historico.sql`: id `bigint generated always as identity` + produto_normalizado, mercado_id, unidade_medida_id, preco_unitario numeric(15,2), data + auditoria.
2. `ddl/primary/preco_historico.sql`: `pk_preco_historico`.
3. `ddl/foreign/preco_historico.sql` e `ddl/index/preco_historico.sql`: fks mercado/unidade; ix_preco_historico_produto, ix_preco_historico_produto_mercado.
4. `dml/inserts/preco_historico.sql`: seed, se houver.

## Onde mexer
- `contas-domesticas-db/ddl/{tables,primary,foreign,index}/preco_historico.sql`

## Critério de pronto (DoD)
- [ ] Scripts refletem o Flyway V17; nomes `pk_`/`uk_`/`ix_`/`fk_` consistentes

## Como testar
Conferir contra a migração V17; rodar em banco limpo.
