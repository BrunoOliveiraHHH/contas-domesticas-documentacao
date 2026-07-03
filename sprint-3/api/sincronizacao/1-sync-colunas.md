# Tarefa — Colunas de sincronização (migração V22) · API
> Sprint 3 (05/08–19/08/2026) · Bloco: Sincronização · Passo 1 · Depende: entidades de domínio

## O que fazer
Adicionar identidade estável e controle de versão às entidades sincronizáveis.

## Passo a passo
1. Migração `V22`: adicionar `uuid`, `versao`, `atualizado_em`, `deletado` (soft-delete) às tabelas de domínio.
2. Índice por `atualizado_em`; único por `uuid`. Espelhar no db.

## Onde mexer
- `.../db/migration/V22__colunas_sincronizacao.sql`, entidades de domínio

## Critério de pronto (DoD)
- [ ] Flyway aplica V22; entidades expõem os novos campos

## Como testar
Subir em dev; conferir colunas/índices.
