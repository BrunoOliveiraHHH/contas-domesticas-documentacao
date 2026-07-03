# Tarefa — Testes: Carteira · API
> Sprint 1 (06/07–20/07/2026) · Bloco: Carteiras · Item: Carteira · Passo 6/6 · Depende: Passos 2–5

## O que fazer
Fechar a cobertura automatizada do Carteira (repository, service, controller).

## Passo a passo
1. `CarteiraRepositoryTest` (`@DataJpaTest`): persistência e queries.
2. `CarteiraServiceTest` (Mockito): regra de visibilidade por dono, bloqueio de remoção com lançamentos, exigir dono quando INDIVIDUAL.
3. `CarteiraControllerIntegrationTest` (`MockMvc`): CRUD + erros.

## Onde mexer
- `src/test/java/br/com/contasdomesticas/api/**/Carteira*Test.java`

## Critério de pronto (DoD)
- [ ] `mvn verify` (profile test, H2) verde
- [ ] Cenários de erro cobertos (404/409/400)

## Como testar
`mvn verify` com Maven local + truststore Norton.
