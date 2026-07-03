# Tarefa — Sincronização: worker (WorkManager) · App
> Sprint 3 (05/08–19/08/2026) · Bloco: Sincronização · Passo 1/2 · Depende: features de domínio, API sync

## O que fazer
Sincronizar Room x API em background.

## Passo a passo
1. `WorkManager` (sync periódico + on-demand); delta por `atualizado_em`; upsert por `uuid`.
2. Indicador de "última sincronização".

## Onde mexer
- `data/sync/*`

## Critério de pronto (DoD)
- [ ] Dados de um device aparecem no outro após sync

## Como testar
Verificação estática + build no Android Studio.
