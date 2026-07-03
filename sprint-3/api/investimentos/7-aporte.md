# Tarefa — Aportes e resgates (saldo aplicado) · API
> Sprint 3 (05/08–19/08/2026) · Bloco: Investimentos · Item Aporte · Depende: Investimento

## O que fazer
Registrar aportes/resgates e calcular o saldo aplicado.

## Passo a passo
1. Migração `V20` da tabela `aporte` (investimento_id, valor, data, tipo APORTE/RESGATE); espelhar no db.
2. `domain/Aporte` + repositório.
3. `/api/v1/investimentos/{id}/aportes` (CRUD); saldo aplicado = soma aportes - soma resgates.

## Onde mexer
- `.../db/migration/V19__*.sql`, `.../domain/Aporte`, `.../service/InvestimentoService`

## Critério de pronto (DoD)
- [ ] CRUD de aportes; saldo aplicado correto

## Como testar
`InvestimentoServiceTest.deveCalcularSaldoAplicado`.
