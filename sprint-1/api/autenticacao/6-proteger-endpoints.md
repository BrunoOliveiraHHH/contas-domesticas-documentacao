# Tarefa — Proteger endpoints (SecurityConfig) · API
> Sprint 1 (06/07–20/07/2026) · Bloco: Autenticação · Passo 6/7 · Depende: Passos 3 e 4

## O que fazer
Trocar o `permitAll` temporário por autorização real com JWT.

## Passo a passo
1. No `SecurityConfig`, usar `authorizeHttpRequests`: público `/api/v1/auth/**`, `/actuator/health`, `/swagger-ui/**`, `/v3/api-docs/**`; resto autenticado.
2. Registrar o `JwtAuthenticationFilter` antes do `UsernamePasswordAuthenticationFilter`.
3. Ajustar os testes de integração existentes para autenticar.

## Onde mexer
- `br.com.contasdomesticas.api.config.SecurityConfig`

## Critério de pronto (DoD)
- [ ] Sem token em rota protegida → 401; com token → 200
- [ ] Auditoria grava o usuário autenticado

## Como testar
`SecurityIntegrationTest`: bloquear sem token, permitir com token, endpoints públicos.
