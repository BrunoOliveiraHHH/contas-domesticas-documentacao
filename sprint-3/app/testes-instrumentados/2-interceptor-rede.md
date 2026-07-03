# Tarefa — Testes instrumentados: interceptor e rede · App
> Sprint 3 (05/08–19/08/2026) · Bloco: Testes instrumentados · Passo 2/3 · Depende: AuthInterceptor, AuditoriaInterceptor

## O que fazer
Testar interceptors com MockWebServer.

## Passo a passo
1. `AuditoriaInterceptor` grava a cada chamada; `AuthInterceptor` injeta token e renova no 401.

## Onde mexer
- `androidTest/.../remote/*`

## Critério de pronto (DoD)
- [ ] Cada chamada gera auditoria; token injetado; renovação no 401

## Como testar
`./gradlew connectedCheck`.
