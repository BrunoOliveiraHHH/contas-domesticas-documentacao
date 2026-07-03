# Tarefa — Serviço + Store: Forma de Pagamento · Frontend
> Sprint 1 (06/07–20/07/2026) · Bloco: Cadastros · Item: Forma de Pagamento · Passo 1/3 · Depende: base do front

## O que fazer
Criar o serviço Axios e o store Pinia de Forma de Pagamento.

## Passo a passo
1. `src/services/forma-pagamento.js`: funções `listar/obter/criar/atualizar/remover` chamando `/api/v1/formas-pagamento`.
2. `src/stores/forma-pagamento.js` (Pinia): estado (itens, carregando, erro) + actions que usam o serviço.

## Onde mexer
- `src/services/forma-pagamento.js`, `src/stores/forma-pagamento.js`

## Critério de pronto (DoD)
- [ ] Store expõe os dados e as ações de CRUD
- [ ] Erros tratados (Notify)

## Como testar
Vitest (store/serviço mockando Axios) + `quasar dev`.
