# Tarefa — Calculadora IR sobre investimentos: cálculo (puro) · App
> Sprint 3 (05/08–19/08/2026) · Bloco: Calculadoras · Item: IR sobre investimentos · Passo 1/2 · Depende: parâmetros da Config

## O que fazer
Implementar o cálculo puro (JVM, sem device) da calculadora de IR sobre investimentos.

## Passo a passo
1. Função de cálculo em `domain/calc/`. Entradas: valor aplicado, rendimento, dias. Saídas: alíquota IR + IOF, imposto e valor líquido.
2. Consumir parâmetros da Configuração quando necessário.

## Onde mexer
- `domain/calc/ir`

## Critério de pronto (DoD)
- [ ] Resultado confere com cálculo manual

## Como testar
Teste unitário do cálculo (JVM).
