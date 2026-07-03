# Tarefa — Relatório: acerto de rateio · API
> Sprint 3 (05/08–19/08/2026) · Bloco: Relatórios · Item Acerto de rateio · Depende: Rateio

## O que fazer
Expor `GET /api/v1/relatorios/rateio?periodo=YYYY-MM` (líquido por usuário + sugestão de acerto).

## Passo a passo
1. Consolidar os rateios do período; algoritmo de minimização de transferências.

## Onde mexer
- `.../service/RelatorioRateioService`, `.../controller/RelatorioController`

## Critério de pronto (DoD)
- [ ] Líquido por usuário correto; menor número de transferências

## Como testar
`RelatorioRateioServiceTest`.
