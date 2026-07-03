# Tarefa — Sessão: logout + guarda de rota · App
> Sprint 1 (06/07–20/07/2026) · Bloco: Login · Passo 4/4 · Depende: tela de login

## O que fazer
Encerrar sessão e proteger as rotas autenticadas.

## Passo a passo
1. `logout` limpa token e volta ao login.
2. Guarda de rota redireciona ao login sem token.

## Onde mexer
- navegação Compose, `SessionManager`

## Critério de pronto (DoD)
- [ ] Logout efetivo; rota protegida sem token redireciona

## Como testar
Verificação estática + build no Android Studio.
