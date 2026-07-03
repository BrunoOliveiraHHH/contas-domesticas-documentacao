# Tarefa — Testes: Investimento · API
> Sprint 3 (05/08–19/08/2026) · Bloco: Investimentos · Item: Investimento · Passo 6/6 · Depende: Passos 2–5

## O que fazer
Fechar a cobertura automatizada do Investimento (repository, service, controller).

## Passo a passo
1. `InvestimentoRepositoryTest` (`@DataJpaTest`): persistência e queries.
2. `InvestimentoServiceTest` (Mockito): CRUD e busca por carteira.
3. `InvestimentoControllerIntegrationTest` (`MockMvc`): CRUD + erros.

## Onde mexer
- `src/test/java/br/com/contasdomesticas/api/**/Investimento*Test.java`

## Critério de pronto (DoD)
- [ ] `mvn verify` (profile test, H2) verde
- [ ] Cenários de erro cobertos (404/409/400)

## Como testar
`mvn verify` com Maven local + truststore Norton.
