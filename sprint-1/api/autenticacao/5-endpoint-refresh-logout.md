# Tarefa — Endpoint de refresh e logout · API
> Sprint 1 (06/07–20/07/2026) · Bloco: Autenticação · Passo 5/7 · Depende: Passo 4 (login)

## O que fazer
Criar `POST /api/v1/auth/refresh` e `POST /api/v1/auth/logout`.

## Passo a passo
1. `AuthService.refresh(refreshToken)`: valida e reemite o par.
2. `AuthService.logout(...)`: encerra a sessão (denylist opcional — decidir na análise).
3. Endpoints no `AuthController`.

## Onde mexer
- `br.com.contasdomesticas.api.controller.AuthController`
- `br.com.contasdomesticas.api.service.AuthService`

## Critério de pronto (DoD)
- [ ] Refresh válido gera novo access; expirado → 401

## Como testar
`AuthControllerIntegrationTest`: refresh válido e expirado.
