# Tarefa — Testes: ItemCompra · API
> Sprint 3 (05/08–19/08/2026) · Bloco: Compras · Item: ItemCompra · Passo 6/6 · Depende: Passos 2–5

## O que fazer
Fechar a cobertura automatizada do ItemCompra (repository, service, controller).

## Passo a passo
1. `ItemCompraRepositoryTest` (`@DataJpaTest`): persistência e queries.
2. `ItemCompraServiceTest` (Mockito): preço a partir do estabelecimento escolhido; regra de comprado.
3. `ItemCompraControllerIntegrationTest` (`MockMvc`): CRUD + erros.

## Onde mexer
- `src/test/java/br/com/contasdomesticas/api/**/ItemCompra*Test.java`

## Critério de pronto (DoD)
- [ ] `mvn verify` (profile test, H2) verde
- [ ] Cenários de erro cobertos (404/409/400)

## Como testar
`mvn verify` com Maven local + truststore Norton.
