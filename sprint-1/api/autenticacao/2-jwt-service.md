# Tarefa — Criar JwtService · API
> Sprint 1 (06/07–20/07/2026) · Bloco: Autenticação · Passo 2/7 · Depende: Passo 1 (JwtProperties)

## O que fazer
Criar o serviço que gera e valida os tokens (HS256).

## Passo a passo
1. Criar `security/JwtService.java`.
2. `gerarAccess(Usuario)` e `gerarRefresh(Usuario)` usando o `secret` e as expirações.
3. `validar(token)` e `extrairLogin(token)`; tratar expirado/assinatura inválida.

## Onde mexer
- `br.com.contasdomesticas.api.security.JwtService`

## Critério de pronto (DoD)
- [ ] Gera e valida token; extrai o login
- [ ] Token expirado/adulterado é rejeitado

## Como testar
`JwtServiceTest`: round-trip gerar→validar, expirado, assinatura adulterada.
