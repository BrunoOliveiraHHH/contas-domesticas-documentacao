# Tarefa — Testes de autenticação · API
> Sprint 1 (06/07–20/07/2026) · Bloco: Autenticação · Passo 7/7 · Depende: Passos 1–6

## O que fazer
Fechar a cobertura do fluxo de autenticação.

## Passo a passo
1. `JwtServiceTest`, `JwtAuthenticationFilterTest`.
2. `AuthControllerIntegrationTest` (login/refresh/logout).
3. `SecurityIntegrationTest` (proteção).

## Onde mexer
- `src/test/java/br/com/contasdomesticas/api/security/**`, `.../auth/**`

## Critério de pronto (DoD)
- [ ] `mvn verify` verde com os novos testes

## Como testar
`mvn verify` (Maven local + truststore Norton).
