# Tarefa — Serviço + Store: Produto · Frontend
> Sprint 1 (06/07–20/07/2026) · Bloco: Cadastros · Item: Produto · Passo 1/3 · Depende: base do front

## O que fazer
Criar o serviço Axios e o store Pinia de Produto.

## Passo a passo
1. `src/services/produto.js`: funções `listar/obter/criar/atualizar/remover` chamando `/api/v1/produtos`.
2. `src/stores/produto.js` (Pinia): estado (itens, carregando, erro) + actions que usam o serviço.

## Onde mexer
- `src/services/produto.js`, `src/stores/produto.js`

## Critério de pronto (DoD)
- [ ] Store expõe os dados e as ações de CRUD
- [ ] Erros tratados (Notify)

## Como testar
Vitest (store/serviço mockando Axios) + `quasar dev`.
