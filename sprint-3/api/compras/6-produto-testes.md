# Tarefa — Testes: Produto · API
> Sprint 3 (05/08–19/08/2026) · Bloco: Compras · Item: Produto · Passo 6/6 · Depende: Passos 2–5

## O que fazer
Fechar a cobertura automatizada do Produto (repository, service, controller).

## Passo a passo
1. `ProdutoRepositoryTest` (`@DataJpaTest`): persistência e queries.
2. `ProdutoServiceTest` (Mockito): CRUD; busca por nome/categoria; produto reaproveitado em várias listas.
3. `ProdutoControllerIntegrationTest` (`MockMvc`): CRUD + erros.

## Onde mexer
- `src/test/java/br/com/contasdomesticas/api/**/Produto*Test.java`

## Critério de pronto (DoD)
- [ ] `mvn verify` (profile test, H2) verde
- [ ] Cenários de erro cobertos (404/409/400)

## Como testar
`mvn verify` com Maven local + truststore Norton.
