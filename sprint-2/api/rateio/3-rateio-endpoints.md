# Tarefa — Endpoints de rateio e acerto · API
> Sprint 2 (21/07–04/08/2026) · Bloco: Rateio · Passo 3 · Depende: service de rateio

## O que fazer
Expor a definição de rateio e o acerto do mês.

## Passo a passo
1. `POST /api/v1/despesas/{id}/rateio`.
2. `GET /api/v1/rateios/acerto?periodo=YYYY-MM` (líquido por usuário).

## Onde mexer
- `.../controller/RateioController`

## Critério de pronto (DoD)
- [ ] Rateio válido salvo; acerto retorna o líquido por usuário

## Como testar
`RateioControllerIntegrationTest`.
