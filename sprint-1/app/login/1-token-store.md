# Tarefa — Armazenamento seguro do token · App
> Sprint 1 (06/07–20/07/2026) · Bloco: Login · Passo 1/4 · Depende: API auth

## O que fazer
Guardar o token com segurança.

## Passo a passo
1. `TokenStore` sobre DataStore + security-crypto (access/refresh + expiração).
2. Métodos salvar/ler/limpar.

## Onde mexer
- `data/auth/TokenStore.kt`

## Critério de pronto (DoD)
- [ ] Token persiste criptografado; limpar no logout

## Como testar
Verificação estática + build; futuro teste instrumentado.
