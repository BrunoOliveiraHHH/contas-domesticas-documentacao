# Tarefa — Tabela `lancamento` (DDL) · DB
> Sprint 1 (06/07–20/07/2026) · Bloco: Lançamentos · Item: lancamento · Depende: espelha Flyway V11 da API

## O que fazer
Criar os scripts DDL separados de `lancamento`, espelho da migração Flyway **V11** da API.

## Passo a passo
1. `ddl/tables/lancamento.sql` — `create table lancamento`: id `bigint generated always as identity` + tipo, descricao, valor numeric(15,2), data_competencia, data_vencimento, data_pagamento, status, carteira_id, categoria_id, forma_pagamento_id, observacao, anexo_url, recorrencia_id, grupo_parcela uuid + auditoria (`criado_em/por`, `atualizado_em/por`).
2. `ddl/primary/lancamento.sql` — `pk_lancamento`.
3. `ddl/foreign/lancamento.sql` e `ddl/index/lancamento.sql` — fks carteira/categoria/forma_pagamento/recorrencia; ix competencia, carteira, tipo_status.
4. `dml/inserts/lancamento.sql` — seed, se houver.

## Onde mexer
- `contas-domesticas-db/ddl/{tables,primary,foreign,index}/lancamento.sql`

## Critério de pronto (DoD)
- [ ] Scripts refletem o Flyway V11 (tipos, nomes, constraints)
- [ ] Nomes `pk_`/`uk_`/`ix_`/`fk_` consistentes

## Como testar
Conferir contra a migração `V11` da API; rodar os scripts em banco limpo (ordem tables→primary→foreign→index→inserts).
