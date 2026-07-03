# Tarefa — Testes: UnidadeMedida · API
> Sprint 1 (06/07–20/07/2026) · Bloco: Cadastros · Item: UnidadeMedida · Passo 6/6 · Depende: Passos 2–5

## O que fazer
Fechar a cobertura automatizada do UnidadeMedida (repository, service, controller).

## Passo a passo
1. `UnidadeMedidaRepositoryTest` (`@DataJpaTest`): persistência e queries.
2. `UnidadeMedidaServiceTest` (Mockito): normalização por fator, sigla duplicada → 409.
3. `UnidadeMedidaControllerIntegrationTest` (`MockMvc`): CRUD + erros.

## Onde mexer
- `src/test/java/br/com/contasdomesticas/api/**/UnidadeMedida*Test.java`

## Critério de pronto (DoD)
- [ ] `mvn verify` (profile test, H2) verde
- [ ] Cenários de erro cobertos (404/409/400)

## Como testar
`mvn verify` com Maven local + truststore Norton.
