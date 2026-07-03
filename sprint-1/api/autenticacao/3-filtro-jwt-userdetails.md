# Tarefa — Filtro JWT + UsuarioDetailsService · API
> Sprint 1 (06/07–20/07/2026) · Bloco: Autenticação · Passo 3/7 · Depende: Passo 2 (JwtService)

## O que fazer
Criar o filtro que autentica pela requisição e o carregador de usuário.

## Passo a passo
1. `security/UsuarioDetailsService.java` (`UserDetailsService`): carrega `Usuario` por login.
2. `security/JwtAuthenticationFilter.java` (`OncePerRequestFilter`): lê `Authorization: Bearer`, valida e popula o `SecurityContext`.
3. Sem header → segue anônimo (não bloqueia aqui).

## Onde mexer
- `br.com.contasdomesticas.api.security.UsuarioDetailsService`
- `br.com.contasdomesticas.api.security.JwtAuthenticationFilter`

## Critério de pronto (DoD)
- [ ] Header válido popula o contexto; ausente segue sem erro

## Como testar
`JwtAuthenticationFilterTest`: header válido/ausente/expirado.
