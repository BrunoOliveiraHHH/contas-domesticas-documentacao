# Tarefa — Configurar JwtProperties · API
> Sprint 1 (06/07–20/07/2026) · Bloco: Autenticação · Passo 1/7 · Depende: base do projeto

## O que fazer
Criar o binding das configurações de JWT que já estão no `application.yml`.

## Passo a passo
1. Criar `security/JwtProperties.java` com `@ConfigurationProperties("app.security.jwt")`.
2. Campos: `secret`, `accessExpiration`, `refreshExpiration`.
3. Habilitar com `@EnableConfigurationProperties(JwtProperties.class)`.

## Onde mexer
- `br.com.contasdomesticas.api.security.JwtProperties`

## Critério de pronto (DoD)
- [ ] Propriedades carregam do `application.yml`
- [ ] App sobe sem erro de binding

## Como testar
Teste de contexto (`@SpringBootTest`) lê as propriedades esperadas.
