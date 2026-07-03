# Tarefa — Tabela `unidade_medida` (DDL) · DB
> Sprint 1 (06/07–20/07/2026) · Bloco: Cadastros · Item: unidade_medida · Depende: espelha Flyway V8 da API

## O que fazer
Criar os scripts DDL separados de `unidade_medida`, espelho da migração Flyway **V8** da API.

## Passo a passo
1. `ddl/tables/unidade_medida.sql` — `create table unidade_medida`: id `bigint generated always as identity` + nome, sigla, tipo, fator_para_base numeric(12,6) + auditoria (`criado_em/por`, `atualizado_em/por`).
2. `ddl/primary/unidade_medida.sql` — `pk_unidade_medida`.
3. `ddl/foreign/unidade_medida.sql` e `ddl/index/unidade_medida.sql` — uk_unidade_medida_sigla (único).
4. `dml/inserts/unidade_medida.sql` — seed, se houver.

## Onde mexer
- `contas-domesticas-db/ddl/{tables,primary,foreign,index}/unidade_medida.sql`

## Critério de pronto (DoD)
- [ ] Scripts refletem o Flyway V8 (tipos, nomes, constraints)
- [ ] Nomes `pk_`/`uk_`/`ix_`/`fk_` consistentes

## Como testar
Conferir contra a migração `V8` da API; rodar os scripts em banco limpo (ordem tables→primary→foreign→index→inserts).
