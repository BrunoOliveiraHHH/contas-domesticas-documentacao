# Tarefa — Relatório: saldo do mês · API
> Sprint 3 (05/08–19/08/2026) · Bloco: Relatórios · Item Saldo · Depende: Receita, Despesa

## O que fazer
Expor `GET /api/v1/relatorios/saldo?periodo=YYYY-MM&carteira=&escopo=` (receita - despesa).

## Passo a passo
1. Serviço de agregação por competência (respeita carteira/escopo).
2. Separar realizado (pago) de previsto (pendente).

## Onde mexer
- `.../service/RelatorioSaldoService`, `.../controller/RelatorioController`

## Critério de pronto (DoD)
- [ ] Totais de receita/despesa/saldo corretos; realizado x previsto separados

## Como testar
`RelatorioSaldoServiceTest`.
