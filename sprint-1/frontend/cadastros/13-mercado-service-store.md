# Tarefa — Serviço + Store: Mercado · Frontend
> Sprint 1 (06/07–20/07/2026) · Bloco: Cadastros · Item: Mercado · Passo 1/3 · Depende: base do front

## O que fazer
Criar o serviço Axios e o store Pinia de Mercado.

## Passo a passo
1. `src/services/mercado.js`: funções `listar/obter/criar/atualizar/remover` chamando `/api/v1/mercados`.
2. `src/stores/mercado.js` (Pinia): estado (itens, carregando, erro) + actions que usam o serviço.

## Onde mexer
- `src/services/mercado.js`, `src/stores/mercado.js`

## Critério de pronto (DoD)
- [ ] Store expõe os dados e as ações de CRUD
- [ ] Erros tratados (Notify)

## Como testar
Vitest (store/serviço mockando Axios) + `quasar dev`.
