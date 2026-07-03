# Tarefa — Entidade + Service (igual/proporcional/custom) · API
> Sprint 2 (21/07–04/08/2026) · Bloco: Rateio · Passo 2 · Depende: migração V14

## O que fazer
Criar as entidades e o serviço de rateio.

## Passo a passo
1. `domain/Rateio` + `domain/ParticipanteRateio` + repositórios.
2. `RateioService`: validar soma (=100% ou =total); PROPORCIONAL usa a renda do período como peso.

## Onde mexer
- `.../domain/Rateio`, `.../service/RateioService`

## Critério de pronto (DoD)
- [ ] Soma inválida = 400; proporcional usa a renda

## Como testar
`RateioServiceTest`: igual/proporcional/custom + soma inválida.
