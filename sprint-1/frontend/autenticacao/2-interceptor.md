# Tarefa — Interceptor Axios (Bearer + refresh) · Frontend
> Sprint 1 (06/07–20/07/2026) · Bloco: Autenticação · Passo 2/4 · Depende: store de auth, api-auth

## O que fazer
Injetar o token e renovar no 401.

## Passo a passo
1. Interceptor de request: adiciona `Authorization: Bearer` a partir do store.
2. Interceptor de response: no 401, chama `/auth/refresh` e repete; se falhar, logout.

## Onde mexer
- `src/boot/axios.js` (interceptors), `src/stores/auth.js`

## Critério de pronto (DoD)
- [ ] Token injetado; renovação automática no 401

## Como testar
Vitest (mock 401 → refresh) + `quasar dev`.
