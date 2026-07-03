# Tarefa — Calculadora de Investimento · Frontend
> Sprint 2 (21/07–04/08/2026) · Bloco: Calculadoras · Item Investimento · Depende: config (índices)

## O que fazer
Projeção de juros compostos com aportes.

## Passo a passo
1. Composable `useCalcInvestimento` (cálculo puro): valor inicial, aporte, taxa (% a.a. ou % CDI/Selic), prazo → valor futuro, total investido, rendimento bruto/líquido.
2. Página com o formulário e o resultado.

## Onde mexer
- `src/composables/useCalcInvestimento.js`, `src/pages/calc/*`

## Critério de pronto (DoD)
- [ ] Resultado confere com juros compostos; usa índice da Config

## Como testar
Vitest (composable) + `quasar dev`.
