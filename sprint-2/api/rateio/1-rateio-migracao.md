# Tarefa — Migração Flyway: rateio + participante_rateio · API
> Sprint 2 (21/07–04/08/2026) · Bloco: Rateio · Passo 1 · Depende: Despesa

## O que fazer
Criar a migração `V14` das tabelas `rateio` e `participante_rateio` e espelhar no db.

## Passo a passo
1. `V14__cria_tabelas_rateio.sql`: `rateio` (lancamento_id, tipo IGUAL/PROPORCIONAL/CUSTOM) + `participante_rateio` (usuario_id, percentual, valor).
2. FKs e espelho no repo db.

## Onde mexer
- `.../db/migration/V14__*.sql`, `contas-domesticas-db/ddl/*`

## Critério de pronto (DoD)
- [ ] Flyway aplica V14

## Como testar
Subir em dev.
