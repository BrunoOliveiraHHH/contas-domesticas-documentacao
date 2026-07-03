# Tarefa — Serviço + Store: Investimento · Frontend
> Sprint 2 (21/07–04/08/2026) · Bloco: Investimentos · Item: Investimento · Passo 1/3 · Depende: base do front

## O que fazer
Criar o serviço Axios e o store Pinia de Investimento.

## Passo a passo
1. `src/services/investimento.js`: funções `listar/obter/criar/atualizar/remover` chamando `/api/v1/investimentos`.
2. `src/stores/investimento.js` (Pinia): estado (itens, carregando, erro) + actions que usam o serviço.

## Onde mexer
- `src/services/investimento.js`, `src/stores/investimento.js`

## Critério de pronto (DoD)
- [ ] Store expõe os dados e as ações de CRUD
- [ ] Erros tratados (Notify)

## Como testar
Vitest (store/serviço mockando Axios) + `quasar dev`.
