# Tarefa — Serviço + Store: Despesa · Frontend
> Sprint 2 (21/07–04/08/2026) · Bloco: Lançamentos · Item: Despesa · Passo 1/3 · Depende: base do front

## O que fazer
Criar o serviço Axios e o store Pinia de Despesa.

## Passo a passo
1. `src/services/despesa.js`: funções `listar/obter/criar/atualizar/remover` chamando `/api/v1/despesas`.
2. `src/stores/despesa.js` (Pinia): estado (itens, carregando, erro) + actions que usam o serviço.

## Onde mexer
- `src/services/despesa.js`, `src/stores/despesa.js`

## Critério de pronto (DoD)
- [ ] Store expõe os dados e as ações de CRUD
- [ ] Erros tratados (Notify)

## Como testar
Vitest (store/serviço mockando Axios) + `quasar dev`.
