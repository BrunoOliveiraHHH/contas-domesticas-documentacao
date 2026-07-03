# Tarefa — Endpoint de parâmetros para calculadoras · API
> Sprint 3 (05/08–19/08/2026) · Bloco: Investimentos · Item Suporte calculadoras · Depende: Parâmetros, Alíquotas

## O que fazer
Expor num contrato único os parâmetros que as calculadoras do app consomem.

## Passo a passo
1. `GET /api/v1/calculadoras/parametros`: índices vigentes (Selic/CDI/IPCA) + faixas de IR/IOF.

## Onde mexer
- `.../controller/CalculadoraController`, `.../service` de parâmetros

## Critério de pronto (DoD)
- [ ] Retorna todos os parâmetros vigentes num payload; reflete alterações

## Como testar
`CalculadoraControllerIntegrationTest.deveRetornarParametros`.
