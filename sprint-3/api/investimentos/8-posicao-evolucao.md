# Tarefa — Posição e evolução patrimonial · API
> Sprint 3 (05/08–19/08/2026) · Bloco: Investimentos · Item Posição/evolução · Depende: Investimento, Aporte, índices

## O que fazer
Registrar posições e expor a evolução e o patrimônio consolidado.

## Passo a passo
1. Migração `V21` da tabela `posicao_investimento` (investimento_id, data, saldo_bruto, rendimento_acumulado); espelhar no db.
2. `GET /api/v1/investimentos/{id}/evolucao` e `GET /api/v1/investimentos/patrimonio?data=`.
3. Estimar rendimento pelo índice vigente quando não houver saldo informado.

## Onde mexer
- `.../db/migration/V20__*.sql`, `.../service/PosicaoService`

## Critério de pronto (DoD)
- [ ] Evolução por investimento e patrimônio consolidado por data

## Como testar
`PosicaoServiceTest`: evolução + estimativa por índice.
