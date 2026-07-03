# Tarefa — Calculadora Financiamento (Price/SAC): cálculo (puro) · App
> Sprint 3 (05/08–19/08/2026) · Bloco: Calculadoras · Item: Financiamento (Price/SAC) · Passo 1/2 · Depende: parâmetros da Config

## O que fazer
Implementar o cálculo puro (JVM, sem device) da calculadora de Financiamento (Price/SAC).

## Passo a passo
1. Função de cálculo em `domain/calc/`. Entradas: valor, taxa a.m., prazo. Saídas: tabela Price e SAC, total de juros, custo total.
2. Consumir parâmetros da Configuração quando necessário.

## Onde mexer
- `domain/calc/financiamento`

## Critério de pronto (DoD)
- [ ] Resultado confere com cálculo manual

## Como testar
Teste unitário do cálculo (JVM).
