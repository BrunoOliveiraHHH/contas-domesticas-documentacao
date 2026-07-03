# Tarefa — Alíquotas de imposto (IR/IOF) parametrizáveis · API
> Sprint 2 (21/07–04/08/2026) · Bloco: Parâmetros & Configuração · Item Alíquotas · Depende: Parametro

## O que fazer
Disponibilizar as faixas de IR regressivo e IOF, configuráveis, e resolver a alíquota por prazo.

## Passo a passo
1. Modelar as faixas: reusar `Parametro` (chaves IR_ATE_180, IR_181_360, IR_361_720, IR_ACIMA_720, IOF_TABELA) ou entidade `FaixaImposto` (decidir na análise).
2. Seed das faixas (22,5 / 20 / 17,5 / 15 e IOF).
3. `GET /api/v1/parametros/impostos` e serviço `resolverAliquota(dias)`.

## Onde mexer
- `service/ImpostoService` (+ entidade `FaixaImposto` se adotada)

## Critério de pronto (DoD)
- [ ] Alíquota correta por faixa de dias (ex.: 200d = 20%, 800d = 15%)
- [ ] Faixas contíguas/sem sobreposição validadas

## Como testar
`ImpostoServiceTest`: resolução por dias; rejeição de faixas sobrepostas.
