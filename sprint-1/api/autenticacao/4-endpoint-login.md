# Tarefa — Endpoint de login · API
> Sprint 1 (06/07–20/07/2026) · Bloco: Autenticação · Passo 4/7 · Depende: Passo 2 (JwtService)

## O que fazer
Criar `POST /api/v1/auth/login` que troca credenciais por tokens.

## Passo a passo
1. `dto/LoginRequest.java` (`@NotBlank login/senha`) e `dto/TokenResponse.java`.
2. `service/AuthService.java`: valida senha com `BCryptPasswordEncoder.matches`; gera tokens.
3. `controller/AuthController.java` (`/api/v1/auth`): `login`.
4. Credencial inválida → 401 genérico via `AplicacaoException`.

## Onde mexer
- `br.com.contasdomesticas.api.controller.AuthController`
- `br.com.contasdomesticas.api.service.AuthService`

## Critério de pronto (DoD)
- [ ] Credenciais válidas retornam tokens; inválidas → 401 genérico

## Como testar
`AuthControllerIntegrationTest`: login válido (admin/admin) e inválido.
