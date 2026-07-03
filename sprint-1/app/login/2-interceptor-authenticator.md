# Tarefa — AuthInterceptor + Authenticator · App
> Sprint 1 (06/07–20/07/2026) · Bloco: Login · Passo 2/4 · Depende: token store

## O que fazer
Injetar o token nas chamadas e renovar no 401.

## Passo a passo
1. `AuthInterceptor` injeta `Authorization: Bearer`.
2. `AuthAuthenticator` chama `/auth/refresh` no 401 e repete a chamada.

## Onde mexer
- `data/remote/AuthInterceptor.kt`, `data/remote/AuthAuthenticator.kt`, `NetworkModule`

## Critério de pronto (DoD)
- [ ] Token injetado; renovação automática no 401

## Como testar
Teste instrumentado com MockWebServer (bloco de testes).
