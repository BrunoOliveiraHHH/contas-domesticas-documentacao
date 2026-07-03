# Tarefa — Testes: Parametro · API
> Sprint 2 (21/07–04/08/2026) · Bloco: Parâmetros & Configuração · Item: Parametro · Passo 6/6 · Depende: Passos 2–5

## O que fazer
Fechar a cobertura automatizada do Parametro (repository, service, controller).

## Passo a passo
1. `ParametroRepositoryTest` (`@DataJpaTest`): persistência e queries.
2. `ParametroServiceTest` (Mockito): seleção do valor vigente por data.
3. `ParametroControllerIntegrationTest` (`MockMvc`): CRUD + erros.

## Onde mexer
- `src/test/java/br/com/contasdomesticas/api/**/Parametro*Test.java`

## Critério de pronto (DoD)
- [ ] `mvn verify` (profile test, H2) verde
- [ ] Cenários de erro cobertos (404/409/400)

## Como testar
`mvn verify` com Maven local + truststore Norton.
