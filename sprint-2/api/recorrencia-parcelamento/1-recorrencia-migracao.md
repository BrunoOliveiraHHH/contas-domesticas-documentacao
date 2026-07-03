# Tarefa — Migração Flyway: tabela recorrencia · API
> Sprint 2 (21/07–04/08/2026) · Bloco: Recorrência & Parcelamento · Item Recorrência · Passo 1 · Depende: Lançamentos

## O que fazer
Criar a migração `V12` da tabela `recorrencia` e espelhar no db.

## Passo a passo
1. `V12__cria_tabela_recorrencia.sql`: modelo do lançamento + frequencia (MENSAL/SEMANAL/ANUAL), dia_vencimento, data_inicio, data_fim, ativa + auditoria.
2. Espelhar no repo db.

## Onde mexer
- `.../db/migration/V12__cria_tabela_recorrencia.sql` e `contas-domesticas-db/ddl/*`

## Critério de pronto (DoD)
- [ ] Flyway aplica V12

## Como testar
Subir em dev.
