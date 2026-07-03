# Tarefa — Tabela `forma_pagamento` (DDL) · DB
> Sprint 1 (06/07–20/07/2026) · Bloco: Cadastros · Item: forma_pagamento · Depende: espelha Flyway V6 da API

## O que fazer
Criar os scripts DDL separados de `forma_pagamento`, espelho da migração Flyway **V6** da API.

## Passo a passo
1. `ddl/tables/forma_pagamento.sql` — `create table forma_pagamento`: id `bigint generated always as identity` + nome, tipo, carteira_id, dia_fechamento smallint, dia_vencimento smallint, ativa boolean + auditoria (`criado_em/por`, `atualizado_em/por`).
2. `ddl/primary/forma_pagamento.sql` — `pk_forma_pagamento`.
3. `ddl/foreign/forma_pagamento.sql` e `ddl/index/forma_pagamento.sql` — fk_forma_pagamento_carteira → carteira(id).
4. `dml/inserts/forma_pagamento.sql` — seed, se houver.

## Onde mexer
- `contas-domesticas-db/ddl/{tables,primary,foreign,index}/forma_pagamento.sql`

## Critério de pronto (DoD)
- [ ] Scripts refletem o Flyway V6 (tipos, nomes, constraints)
- [ ] Nomes `pk_`/`uk_`/`ix_`/`fk_` consistentes

## Como testar
Conferir contra a migração `V6` da API; rodar os scripts em banco limpo (ordem tables→primary→foreign→index→inserts).
