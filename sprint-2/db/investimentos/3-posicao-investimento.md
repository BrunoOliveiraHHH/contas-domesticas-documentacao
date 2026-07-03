# Tarefa — Tabela `posicao_investimento` (DDL) · DB
> Sprint 2 (21/07–04/08/2026) · Bloco: Investimentos · Item: posicao_investimento · Depende: espelha Flyway V21 da API

## O que fazer
Criar os scripts DDL separados de `posicao_investimento`, espelho da migração Flyway **V21** da API.

## Passo a passo
1. `ddl/tables/posicao_investimento.sql` — `create table posicao_investimento`: id `bigint generated always as identity` + investimento_id, data, saldo_bruto numeric(15,2), rendimento_acumulado numeric(15,2) + auditoria (`criado_em/por`, `atualizado_em/por`).
2. `ddl/primary/posicao_investimento.sql` — `pk_posicao_investimento`.
3. `ddl/foreign/posicao_investimento.sql` e `ddl/index/posicao_investimento.sql` — fk → investimento(id); uk_posicao_investimento_data (investimento_id, data).
4. `dml/inserts/posicao_investimento.sql` — seed, se houver.

## Onde mexer
- `contas-domesticas-db/ddl/{tables,primary,foreign,index}/posicao_investimento.sql`

## Critério de pronto (DoD)
- [ ] Scripts refletem o Flyway V21 (tipos, nomes, constraints)
- [ ] Nomes `pk_`/`uk_`/`ix_`/`fk_` consistentes

## Como testar
Conferir contra a migração `V21` da API; rodar os scripts em banco limpo (ordem tables→primary→foreign→index→inserts).
