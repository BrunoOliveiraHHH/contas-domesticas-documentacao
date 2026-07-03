# Tarefa — Serviço + Store: Receita · Frontend
> Sprint 2 (21/07–04/08/2026) · Bloco: Lançamentos · Item: Receita · Passo 1/3 · Depende: base do front

## O que fazer
Criar o serviço Axios e o store Pinia de Receita.

## Passo a passo
1. `src/services/receita.js`: funções `listar/obter/criar/atualizar/remover` chamando `/api/v1/receitas`.
2. `src/stores/receita.js` (Pinia): estado (itens, carregando, erro) + actions que usam o serviço.

## Onde mexer
- `src/services/receita.js`, `src/stores/receita.js`

## Critério de pronto (DoD)
- [ ] Store expõe os dados e as ações de CRUD
- [ ] Erros tratados (Notify)

## Como testar
Vitest (store/serviço mockando Axios) + `quasar dev`.
