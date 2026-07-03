# Tarefa — Calculadora Investimento: tela + ViewModel · App
> Sprint 3 (05/08–19/08/2026) · Bloco: Calculadoras · Item: Investimento · Passo 2/2 · Depende: Passo 1 (cálculo)

## O que fazer
Construir a tela da calculadora de Investimento.

## Passo a passo
1. `ui/calc/investimentoScreen.kt` (entradas: valor inicial, aporte mensal, taxa (% a.a. ou % CDI/Selic), prazo).
2. `investimentoViewModel` chama o cálculo e exibe: valor futuro, total investido, rendimento bruto e líquido.

## Onde mexer
- `ui/calc/investimentoScreen.kt`, `ui/calc/investimentoViewModel.kt`

## Critério de pronto (DoD)
- [ ] Tela calcula e exibe os resultados

## Como testar
Verificação estática + build no Android Studio.
