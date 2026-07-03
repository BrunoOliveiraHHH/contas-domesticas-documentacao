# Tarefa — Tabela `investimento` (DDL) · DB
> Sprint 2 (21/07–04/08/2026) · Bloco: Investimentos · Item: investimento · Depende: espelha Flyway V19 da API

## O que fazer
Criar os scripts DDL separados de `investimento`, espelho da migração Flyway **V19** da API.

## Passo a passo
1. `ddl/tables/investimento.sql` — `create table investimento`: id `bigint generated always as identity` + nome, tipo_investimento, instituicao, carteira_id, indexador, taxa_contratada numeric(9,4), data_aplicacao, data_vencimento + auditoria (`criado_em/por`, `atualizado_em/por`).
2. `ddl/primary/investimento.sql` — `pk_investimento`.
3. `ddl/foreign/investimento.sql` e `ddl/index/investimento.sql` — fk_investimento_carteira → carteira(id); ix_investimento_tipo.
4. `dml/inserts/investimento.sql` — seed, se houver.

## Onde mexer
- `contas-domesticas-db/ddl/{tables,primary,foreign,index}/investimento.sql`

## Critério de pronto (DoD)
- [ ] Scripts refletem o Flyway V19 (tipos, nomes, constraints)
- [ ] Nomes `pk_`/`uk_`/`ix_`/`fk_` consistentes

## Como testar
Conferir contra a migração `V19` da API; rodar os scripts em banco limpo (ordem tables→primary→foreign→index→inserts).
