# Tarefa — Tabela `categoria` (DDL) · DB
> Sprint 1 (06/07–20/07/2026) · Bloco: Cadastros · Item: categoria · Depende: espelha Flyway V5 da API

## O que fazer
Criar os scripts DDL separados de `categoria`, espelho da migração Flyway **V5** da API.

## Passo a passo
1. `ddl/tables/categoria.sql` — `create table categoria`: id `bigint generated always as identity` + nome, tipo, categoria_pai_id, cor, icone, ativa boolean + auditoria (`criado_em/por`, `atualizado_em/por`).
2. `ddl/primary/categoria.sql` — `pk_categoria`.
3. `ddl/foreign/categoria.sql` e `ddl/index/categoria.sql` — fk_categoria_pai → categoria(id); ix_categoria_tipo, ix_categoria_pai.
4. `dml/inserts/categoria.sql` — seed, se houver.

## Onde mexer
- `contas-domesticas-db/ddl/{tables,primary,foreign,index}/categoria.sql`

## Critério de pronto (DoD)
- [ ] Scripts refletem o Flyway V5 (tipos, nomes, constraints)
- [ ] Nomes `pk_`/`uk_`/`ix_`/`fk_` consistentes

## Como testar
Conferir contra a migração `V5` da API; rodar os scripts em banco limpo (ordem tables→primary→foreign→index→inserts).
