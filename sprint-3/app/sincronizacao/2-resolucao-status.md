# Tarefa — Sincronização: resolução de conflito + status · App
> Sprint 3 (05/08–19/08/2026) · Bloco: Sincronização · Passo 2/2 · Depende: worker, API merge

## O que fazer
Aplicar merge (mais recente vence) e mostrar o status.

## Passo a passo
1. Resolver conflito por `atualizado_em`; soft-delete via tombstone.
2. Badge de pendências não sincronizadas.

## Onde mexer
- `data/sync/*`, `ui/*`

## Critério de pronto (DoD)
- [ ] Conflito resolve pelo mais recente; deleção propaga; UI mostra status

## Como testar
Verificação estática + build no Android Studio.
