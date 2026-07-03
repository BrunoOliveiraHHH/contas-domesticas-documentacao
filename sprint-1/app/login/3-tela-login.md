# Tarefa — Tela de login + AuthGate · App
> Sprint 1 (06/07–20/07/2026) · Bloco: Login · Passo 3/4 · Depende: token store, navegação

## O que fazer
Construir a tela de login e o gate de entrada.

## Passo a passo
1. `LoginScreen` (login/senha, erro, loading) chama `/auth/login`.
2. `AuthGate/Splash` decide login x home pelo token.

## Onde mexer
- `ui/login/LoginScreen.kt`, `ui/login/LoginViewModel.kt`

## Critério de pronto (DoD)
- [ ] Credenciais válidas entram; inválidas mostram erro; sessão persiste

## Como testar
Verificação estática + build; teste de UI no bloco de testes.
