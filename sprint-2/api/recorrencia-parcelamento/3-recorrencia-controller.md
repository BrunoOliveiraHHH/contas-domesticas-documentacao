# Tarefa — Controller + agendamento · API
> Sprint 2 (21/07–04/08/2026) · Bloco: Recorrência & Parcelamento · Item Recorrência · Passo 3 · Depende: service de recorrência

## O que fazer
Expor o CRUD de recorrências e o disparo de geração.

## Passo a passo
1. `RecorrenciaController` (`/api/v1/recorrencias`, CRUD).
2. `POST /{id}/gerar` e/ou `@Scheduled` para gerar o período.

## Onde mexer
- `.../controller/RecorrenciaController`

## Critério de pronto (DoD)
- [ ] CRUD + geração via endpoint funcionam

## Como testar
`RecorrenciaControllerIntegrationTest`.
