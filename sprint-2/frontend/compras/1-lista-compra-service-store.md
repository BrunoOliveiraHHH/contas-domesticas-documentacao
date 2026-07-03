# Tarefa — Serviço + Store: Lista de Compra · Frontend
> Sprint 2 (21/07–04/08/2026) · Bloco: Compras · Item: Lista de Compra · Passo 1/3 · Depende: base do front

## O que fazer
Criar o serviço Axios e o store Pinia de Lista de Compra.

## Passo a passo
1. `src/services/lista-compra.js`: funções `listar/obter/criar/atualizar/remover` chamando `/api/v1/listas-compra`.
2. `src/stores/lista-compra.js` (Pinia): estado (itens, carregando, erro) + actions que usam o serviço.

## Onde mexer
- `src/services/lista-compra.js`, `src/stores/lista-compra.js`

## Critério de pronto (DoD)
- [ ] Store expõe os dados e as ações de CRUD
- [ ] Erros tratados (Notify)

## Como testar
Vitest (store/serviço mockando Axios) + `quasar dev`.
