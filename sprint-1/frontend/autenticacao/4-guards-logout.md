# Tarefa — Route guards + logout · Frontend
> Sprint 1 (06/07–20/07/2026) · Bloco: Autenticação · Passo 4/4 · Depende: login

## O que fazer
Proteger rotas e encerrar sessão.

## Passo a passo
1. `router.beforeEach`: sem token → redireciona a `/login`.
2. Ação de logout (limpa store e volta ao login).

## Onde mexer
- `src/router/index.js`, `src/layouts/MainLayout.vue`

## Critério de pronto (DoD)
- [ ] Rota protegida sem token redireciona; logout efetivo

## Como testar
`quasar dev`.
