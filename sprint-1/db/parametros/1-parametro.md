# Tarefa — Tabela `parametro` (DDL) · DB
> Sprint 1 (06/07–20/07/2026) · Bloco: Parâmetros · Item: parametro · Depende: espelha Flyway V9 da API

## O que fazer
Criar os scripts DDL separados de `parametro`, espelho da migração Flyway **V9** da API.

## Passo a passo
1. `ddl/tables/parametro.sql` — `create table parametro`: id `bigint generated always as identity` + chave, valor numeric(9,4), vigencia_inicio date, descricao + auditoria (`criado_em/por`, `atualizado_em/por`).
2. `ddl/primary/parametro.sql` — `pk_parametro`.
3. `ddl/foreign/parametro.sql` e `ddl/index/parametro.sql` — ix_parametro_chave_vigencia (chave, vigencia_inicio); seed Selic/CDI/IPCA e faixas IR/IOF.
4. `dml/inserts/parametro.sql` — seed, se houver.

## Onde mexer
- `contas-domesticas-db/ddl/{tables,primary,foreign,index}/parametro.sql`

## Critério de pronto (DoD)
- [ ] Scripts refletem o Flyway V9 (tipos, nomes, constraints)
- [ ] Nomes `pk_`/`uk_`/`ix_`/`fk_` consistentes

## Como testar
Conferir contra a migração `V9` da API; rodar os scripts em banco limpo (ordem tables→primary→foreign→index→inserts).
