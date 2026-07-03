# Tarefa — Entidade + Service (geração idempotente) · API
> Sprint 2 (21/07–04/08/2026) · Bloco: Recorrência & Parcelamento · Item Recorrência · Passo 2 · Depende: migração V12

## O que fazer
Criar `Recorrencia` e o serviço que gera os lançamentos sem duplicar.

## Passo a passo
1. `domain/Recorrencia.java` + repositório.
2. `RecorrenciaService.gerar(competencia)` cria `Lancamento` com `recorrencia_id`; idempotente por competência.

## Onde mexer
- `.../domain/Recorrencia`, `.../service/RecorrenciaService`

## Critério de pronto (DoD)
- [ ] Gera 1 lançamento por período; não duplica; respeita vigência

## Como testar
`RecorrenciaServiceTest`: geração idempotente por competência.
