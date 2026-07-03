# Tarefa — Tabela `mercado` (DDL) · DB
> Sprint 1 (06/07–20/07/2026) · Bloco: Cadastros · Item: mercado · Depende: espelha Flyway V7 da API

## O que fazer
Criar os scripts DDL separados de `mercado`, espelho da migração Flyway **V7** da API.

## Passo a passo
1. `ddl/tables/mercado.sql` — `create table mercado`: id `bigint generated always as identity` + nome, tipo, endereco, bairro, ativo boolean + auditoria (`criado_em/por`, `atualizado_em/por`).
2. `ddl/primary/mercado.sql` — `pk_mercado`.
3. `ddl/foreign/mercado.sql` e `ddl/index/mercado.sql` — ix_mercado_tipo.
4. `dml/inserts/mercado.sql` — seed, se houver.

## Onde mexer
- `contas-domesticas-db/ddl/{tables,primary,foreign,index}/mercado.sql`

## Critério de pronto (DoD)
- [ ] Scripts refletem o Flyway V7 (tipos, nomes, constraints)
- [ ] Nomes `pk_`/`uk_`/`ix_`/`fk_` consistentes

## Como testar
Conferir contra a migração `V7` da API; rodar os scripts em banco limpo (ordem tables→primary→foreign→index→inserts).
