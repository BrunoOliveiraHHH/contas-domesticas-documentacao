# Tarefa — Serviço + Store: Unidade de Medida · Frontend
> Sprint 1 (06/07–20/07/2026) · Bloco: Cadastros · Item: Unidade de Medida · Passo 1/3 · Depende: base do front

## O que fazer
Criar o serviço Axios e o store Pinia de Unidade de Medida.

## Passo a passo
1. `src/services/unidade-medida.js`: funções `listar/obter/criar/atualizar/remover` chamando `/api/v1/unidades-medida`.
2. `src/stores/unidade-medida.js` (Pinia): estado (itens, carregando, erro) + actions que usam o serviço.

## Onde mexer
- `src/services/unidade-medida.js`, `src/stores/unidade-medida.js`

## Critério de pronto (DoD)
- [ ] Store expõe os dados e as ações de CRUD
- [ ] Erros tratados (Notify)

## Como testar
Vitest (store/serviço mockando Axios) + `quasar dev`.
