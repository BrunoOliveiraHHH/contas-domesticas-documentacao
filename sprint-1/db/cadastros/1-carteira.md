# Tarefa — Tabela `carteira` (DDL) · DB
> Sprint 1 (06/07–20/07/2026) · Bloco: Cadastros · Item: carteira · Depende: espelha Flyway V4 da API

## O que fazer
Criar os scripts DDL separados de `carteira`, espelho da migração Flyway **V4** da API.

## Passo a passo
1. `ddl/tables/carteira.sql` — `create table carteira`: id `bigint generated always as identity` + nome, tipo (FAMILIAR/INDIVIDUAL), dono_id, saldo_inicial numeric(15,2), moeda varchar(3), cor, icone, ativa boolean + auditoria (`criado_em/por`, `atualizado_em/por`).
2. `ddl/primary/carteira.sql` — `pk_carteira`.
3. `ddl/foreign/carteira.sql` e `ddl/index/carteira.sql` — fk_carteira_dono → usuario(id); ix_carteira_dono, ix_carteira_tipo.
4. `dml/inserts/carteira.sql` — seed, se houver.

## Onde mexer
- `contas-domesticas-db/ddl/{tables,primary,foreign,index}/carteira.sql`

## Critério de pronto (DoD)
- [ ] Scripts refletem o Flyway V4 (tipos, nomes, constraints)
- [ ] Nomes `pk_`/`uk_`/`ix_`/`fk_` consistentes

## Como testar
Conferir contra a migração `V4` da API; rodar os scripts em banco limpo (ordem tables→primary→foreign→index→inserts).
