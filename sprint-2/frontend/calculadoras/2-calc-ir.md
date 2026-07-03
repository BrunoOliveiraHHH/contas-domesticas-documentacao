# Tarefa — Calculadora de IR sobre investimentos · Frontend
> Sprint 2 (21/07–04/08/2026) · Bloco: Calculadoras · Item IR · Depende: config (alíquotas)

## O que fazer
Imposto no resgate de renda fixa.

## Passo a passo
1. Composable de IR: valor aplicado, rendimento, dias → alíquota (22,5→15%) + IOF, imposto e líquido.
2. Página do formulário.

## Onde mexer
- `src/composables/useCalcIr.js`, `src/pages/calc/*`

## Critério de pronto (DoD)
- [ ] Alíquota correta por faixa; IOF nos primeiros 30 dias; líquido exato

## Como testar
Vitest (composable) + `quasar dev`.
