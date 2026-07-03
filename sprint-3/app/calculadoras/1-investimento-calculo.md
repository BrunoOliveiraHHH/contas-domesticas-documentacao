# Tarefa — Calculadora Investimento: cálculo (puro) · App
> Sprint 3 (05/08–19/08/2026) · Bloco: Calculadoras · Item: Investimento · Passo 1/2 · Depende: parâmetros da Config

## O que fazer
Implementar o cálculo puro (JVM, sem device) da calculadora de Investimento.

## Passo a passo
1. Função de cálculo em `domain/calc/`. Entradas: valor inicial, aporte mensal, taxa (% a.a. ou % CDI/Selic), prazo. Saídas: valor futuro, total investido, rendimento bruto e líquido.
2. Consumir parâmetros da Configuração quando necessário.

## Onde mexer
- `domain/calc/investimento`

## Critério de pronto (DoD)
- [ ] Resultado confere com cálculo manual

## Como testar
Teste unitário do cálculo (JVM).
