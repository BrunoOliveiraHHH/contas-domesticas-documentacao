# Tarefa — Endpoints de sincronização (delta + upsert) · API
> Sprint 3 (05/08–19/08/2026) · Bloco: Sincronização · Passo 2 · Depende: colunas de sync

## O que fazer
Expor a troca por deltas.

## Passo a passo
1. `GET /api/v1/sync?desde=<instant>` retorna deltas por entidade.
2. `POST /api/v1/sync` recebe mudanças do cliente (upsert por `uuid`).

## Onde mexer
- `.../controller/SyncController`, `.../service/SyncService`

## Critério de pronto (DoD)
- [ ] Delta retorna só o alterado desde o timestamp; upsert por uuid

## Como testar
`SyncServiceTest` + `SyncControllerIntegrationTest`.
