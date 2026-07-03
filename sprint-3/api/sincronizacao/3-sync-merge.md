# Tarefa — Resolução de conflito (merge LWW) · API
> Sprint 3 (05/08–19/08/2026) · Bloco: Sincronização · Passo 3 · Depende: endpoints de sync

## O que fazer
Aplicar a política de merge (mais recente vence).

## Passo a passo
1. No `POST /sync`, resolver conflito por `atualizado_em` (last-write-wins).
2. `deletado=true` como tombstone (deleção propaga); `versao` detecta conflito.

## Onde mexer
- `.../service/MergeService`

## Critério de pronto (DoD)
- [ ] Conflito resolve pelo mais recente; deleção propaga; sem perda silenciosa

## Como testar
`MergeServiceTest`: LWW, tombstone, versão divergente.
