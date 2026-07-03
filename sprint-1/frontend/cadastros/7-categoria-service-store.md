# Tarefa — Serviço + Store: Categoria · Frontend
> Sprint 1 (06/07–20/07/2026) · Bloco: Cadastros · Item: Categoria · Passo 1/3 · Depende: base do front

## O que fazer
Criar o serviço Axios e o store Pinia de Categoria.

## Passo a passo
1. `src/services/categoria.js`: funções `listar/obter/criar/atualizar/remover` chamando `/api/v1/categorias`.
2. `src/stores/categoria.js` (Pinia): estado (itens, carregando, erro) + actions que usam o serviço.

## Onde mexer
- `src/services/categoria.js`, `src/stores/categoria.js`

## Critério de pronto (DoD)
- [ ] Store expõe os dados e as ações de CRUD
- [ ] Erros tratados (Notify)

## Como testar
Vitest (store/serviço mockando Axios) + `quasar dev`.
