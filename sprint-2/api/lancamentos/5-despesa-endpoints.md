# Tarefa — Despesa: service + controller (status) · API
> Sprint 2 (21/07–04/08/2026) · Bloco: Lançamentos · Item Despesa · Passo 1 · Depende: Lançamento base

## O que fazer
Expor o CRUD de despesas (tipo=DESPESA) com status derivado e ação marcar como pago.

## Passo a passo
1. `DespesaService`: status PAGO/PENDENTE/ATRASADO derivado por data; `marcarComoPago`.
2. `DespesaController` (`/api/v1/despesas`, CRUD + marcar pago).

## Onde mexer
- `.../service/DespesaService`, `.../controller/DespesaController`

## Critério de pronto (DoD)
- [ ] Status calculado por data; marcar pago registra `data_pagamento`

## Como testar
`DespesaServiceTest` (transição de status) + `DespesaControllerIntegrationTest`.
