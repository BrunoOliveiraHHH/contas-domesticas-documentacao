# Tarefa — Receita: service + controller · API
> Sprint 2 (21/07–04/08/2026) · Bloco: Lançamentos · Item Receita · Passo 1 · Depende: Lançamento base

## O que fazer
Expor o CRUD de receitas sobre `Lancamento` (tipo=RECEITA) em `/api/v1/receitas`.

## Passo a passo
1. `ReceitaService` (cria `Lancamento` RECEITA; categoria precisa ser de tipo RECEITA).
2. `ReceitaController` (`/api/v1/receitas`, CRUD).

## Onde mexer
- `.../service/ReceitaService`, `.../controller/ReceitaController`

## Critério de pronto (DoD)
- [ ] CRUD ok; categoria de tipo diferente de RECEITA = 400

## Como testar
`ReceitaControllerIntegrationTest` + `ReceitaServiceTest`.
