# Tarefa — Endpoint de despesa parcelada · API
> Sprint 2 (21/07–04/08/2026) · Bloco: Recorrência & Parcelamento · Item Parcelamento · Passo 2 · Depende: modelo de parcela

## O que fazer
Gerar despesas parceladas com vencimentos e soma corretos.

## Passo a passo
1. `POST /api/v1/despesas/parceladas` com valorTotal, parcelas, primeiroVencimento.
2. Vencimentos a partir do fechamento/vencimento do cartão; ajuste do centavo na última parcela.

## Onde mexer
- `.../service/ParcelamentoService`, `.../controller` (despesas)

## Critério de pronto (DoD)
- [ ] N parcelas; soma = total; vencimentos corretos

## Como testar
`ParcelamentoServiceTest`: geração e arredondamento.
