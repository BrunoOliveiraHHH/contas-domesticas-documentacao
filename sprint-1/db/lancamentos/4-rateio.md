# Tarefa — Tabela `rateio` (DDL) · DB
> Sprint 1 (06/07–20/07/2026) · Bloco: Lançamentos · Item: rateio · Depende: espelha Flyway V14 da API

## O que fazer
Criar os scripts DDL separados de `rateio`, espelho da migração Flyway **V14** da API.

## Passo a passo
1. `ddl/tables/rateio.sql` — `create table rateio`: id `bigint generated always as identity` + rateio (lancamento_id, tipo) + participante_rateio (rateio_id, usuario_id, percentual numeric(7,4), valor numeric(15,2)) + auditoria (`criado_em/por`, `atualizado_em/por`).
2. `ddl/primary/rateio.sql` — `pk_rateio`.
3. `ddl/foreign/rateio.sql` e `ddl/index/rateio.sql` — fks rateio→lancamento, participante→rateio e →usuario (duas tabelas neste script).
4. `dml/inserts/rateio.sql` — seed, se houver.

## Onde mexer
- `contas-domesticas-db/ddl/{tables,primary,foreign,index}/rateio.sql`

## Critério de pronto (DoD)
- [ ] Scripts refletem o Flyway V14 (tipos, nomes, constraints)
- [ ] Nomes `pk_`/`uk_`/`ix_`/`fk_` consistentes

## Como testar
Conferir contra a migração `V14` da API; rodar os scripts em banco limpo (ordem tables→primary→foreign→index→inserts).
