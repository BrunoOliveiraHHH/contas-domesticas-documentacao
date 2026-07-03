# Tarefa — Store de auth + token · Frontend
> Sprint 1 (06/07–20/07/2026) · Bloco: Autenticação · Passo 1/4 · Depende: fundação

## O que fazer
Guardar token e usuário logado.

## Passo a passo
1. `src/stores/auth.js` (Pinia): `token`, `refreshToken`, `usuario`; persistir em `localStorage`.
2. Actions `setTokens/limpar`.

## Onde mexer
- `src/stores/auth.js`

## Critério de pronto (DoD)
- [ ] Token persiste entre reloads; limpar no logout

## Como testar
Vitest (store) + `quasar dev`.
