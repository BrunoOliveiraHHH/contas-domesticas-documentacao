# Tarefa — Testes: Mercado · API
> Sprint 1 (06/07–20/07/2026) · Bloco: Cadastros · Item: Mercado · Passo 6/6 · Depende: Passos 2–5

## O que fazer
Fechar a cobertura automatizada do Mercado (repository, service, controller).

## Passo a passo
1. `MercadoRepositoryTest` (`@DataJpaTest`): persistência e queries.
2. `MercadoServiceTest` (Mockito): filtro por tipo, CRUD e 404.
3. `MercadoControllerIntegrationTest` (`MockMvc`): CRUD + erros.

## Onde mexer
- `src/test/java/br/com/contasdomesticas/api/**/Mercado*Test.java`

## Critério de pronto (DoD)
- [ ] `mvn verify` (profile test, H2) verde
- [ ] Cenários de erro cobertos (404/409/400)

## Como testar
`mvn verify` com Maven local + truststore Norton.
