# Tarefa — Tabela `recorrencia` (DDL) · DB
> Sprint 1 (06/07–20/07/2026) · Bloco: Lançamentos · Item: recorrencia · Depende: espelha Flyway V12 da API

## O que fazer
Criar os scripts DDL separados de `recorrencia`, espelho da migração Flyway **V12** da API.

## Passo a passo
1. `ddl/tables/recorrencia.sql` — `create table recorrencia`: id `bigint generated always as identity` + descricao, valor, tipo, carteira_id, categoria_id, forma_pagamento_id, frequencia, dia_vencimento smallint, data_inicio, data_fim, ativa boolean + auditoria (`criado_em/por`, `atualizado_em/por`).
2. `ddl/primary/recorrencia.sql` — `pk_recorrencia`.
3. `ddl/foreign/recorrencia.sql` e `ddl/index/recorrencia.sql` — fks carteira/categoria/forma_pagamento; ix_recorrencia_ativa.
4. `dml/inserts/recorrencia.sql` — seed, se houver.

## Onde mexer
- `contas-domesticas-db/ddl/{tables,primary,foreign,index}/recorrencia.sql`

## Critério de pronto (DoD)
- [ ] Scripts refletem o Flyway V12 (tipos, nomes, constraints)
- [ ] Nomes `pk_`/`uk_`/`ix_`/`fk_` consistentes

## Como testar
Conferir contra a migração `V12` da API; rodar os scripts em banco limpo (ordem tables→primary→foreign→index→inserts).
