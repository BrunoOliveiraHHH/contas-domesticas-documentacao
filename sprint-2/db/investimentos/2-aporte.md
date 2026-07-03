# Tarefa — Tabela `aporte` (DDL) · DB
> Sprint 2 (21/07–04/08/2026) · Bloco: Investimentos · Item: aporte · Depende: espelha Flyway V19 da API

## O que fazer
Criar os scripts DDL separados de `aporte`, espelho da migração Flyway **V19** da API.

## Passo a passo
1. `ddl/tables/aporte.sql` — `create table aporte`: id `bigint generated always as identity` + investimento_id, valor numeric(15,2), data, tipo (APORTE/RESGATE) + auditoria (`criado_em/por`, `atualizado_em/por`).
2. `ddl/primary/aporte.sql` — `pk_aporte`.
3. `ddl/foreign/aporte.sql` e `ddl/index/aporte.sql` — fk_aporte_investimento (on delete cascade); ix_aporte_investimento_data.
4. `dml/inserts/aporte.sql` — seed, se houver.

## Onde mexer
- `contas-domesticas-db/ddl/{tables,primary,foreign,index}/aporte.sql`

## Critério de pronto (DoD)
- [ ] Scripts refletem o Flyway V19 (tipos, nomes, constraints)
- [ ] Nomes `pk_`/`uk_`/`ix_`/`fk_` consistentes

## Como testar
Conferir contra a migração `V19` da API; rodar os scripts em banco limpo (ordem tables→primary→foreign→index→inserts).
