# Tarefa — Página de login · Frontend
> Sprint 1 (06/07–20/07/2026) · Bloco: Autenticação · Passo 3/4 · Depende: interceptor

## O que fazer
Tela de login que autentica e guarda o token.

## Passo a passo
1. `src/pages/LoginPage.vue` (`QForm`: login/senha) → `POST /auth/login`.
2. Sucesso: grava token no store e redireciona ao dashboard; erro: `Notify`.

## Onde mexer
- `src/pages/LoginPage.vue`, `src/router/routes.js`

## Critério de pronto (DoD)
- [ ] Credenciais válidas entram; inválidas mostram erro; sessão persiste

## Como testar
`quasar dev`; e2e no bloco de testes.
