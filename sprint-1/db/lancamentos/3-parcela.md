# Tarefa — Tabela `parcela` (DDL) · DB
> Sprint 1 (06/07–20/07/2026) · Bloco: Lançamentos · Item: parcela · Depende: espelha Flyway V13 da API

## O que fazer
Criar os scripts DDL separados de `parcela`, espelho da migração Flyway **V13** da API.

## Passo a passo
1. `ddl/tables/parcela.sql` — `create table parcela`: id `bigint generated always as identity` + lancamento_id, numero smallint, total smallint, valor_parcela numeric(15,2), vencimento date, status + auditoria (`criado_em/por`, `atualizado_em/por`).
2. `ddl/primary/parcela.sql` — `pk_parcela`.
3. `ddl/foreign/parcela.sql` e `ddl/index/parcela.sql` — fk_parcela_lancamento → lancamento(id); ix_parcela_vencimento.
4. `dml/inserts/parcela.sql` — seed, se houver.

## Onde mexer
- `contas-domesticas-db/ddl/{tables,primary,foreign,index}/parcela.sql`

## Critério de pronto (DoD)
- [ ] Scripts refletem o Flyway V13 (tipos, nomes, constraints)
- [ ] Nomes `pk_`/`uk_`/`ix_`/`fk_` consistentes

## Como testar
Conferir contra a migração `V13` da API; rodar os scripts em banco limpo (ordem tables→primary→foreign→index→inserts).
