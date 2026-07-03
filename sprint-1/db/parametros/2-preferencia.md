# Tarefa — Tabela `preferencia` (DDL) · DB
> Sprint 1 (06/07–20/07/2026) · Bloco: Parâmetros · Item: preferencia · Depende: espelha Flyway V10 da API

## O que fazer
Criar os scripts DDL separados de `preferencia`, espelho da migração Flyway **V10** da API.

## Passo a passo
1. `ddl/tables/preferencia.sql` — `create table preferencia`: id `bigint generated always as identity` + chave, valor, usuario_id + auditoria (`criado_em/por`, `atualizado_em/por`).
2. `ddl/primary/preferencia.sql` — `pk_preferencia`.
3. `ddl/foreign/preferencia.sql` e `ddl/index/preferencia.sql` — fk_preferencia_usuario → usuario(id); uk_preferencia_chave_usuario (chave, usuario_id).
4. `dml/inserts/preferencia.sql` — seed, se houver.

## Onde mexer
- `contas-domesticas-db/ddl/{tables,primary,foreign,index}/preferencia.sql`

## Critério de pronto (DoD)
- [ ] Scripts refletem o Flyway V10 (tipos, nomes, constraints)
- [ ] Nomes `pk_`/`uk_`/`ix_`/`fk_` consistentes

## Como testar
Conferir contra a migração `V10` da API; rodar os scripts em banco limpo (ordem tables→primary→foreign→index→inserts).
