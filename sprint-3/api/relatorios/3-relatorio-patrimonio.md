# Tarefa — Relatório: evolução patrimonial · API
> Sprint 3 (05/08–19/08/2026) · Bloco: Relatórios · Item Patrimônio · Depende: Posição, Saldo

## O que fazer
Expor `GET /api/v1/relatorios/patrimonio?de=&ate=` (série mensal de saldos + investimentos).

## Passo a passo
1. Agregar posições de investimento + saldos por mês no intervalo.

## Onde mexer
- `.../service/RelatorioPatrimonioService`, `.../controller/RelatorioController`

## Critério de pronto (DoD)
- [ ] Série mensal consistente com posições e saldos

## Como testar
`RelatorioPatrimonioServiceTest`.
