# Tarefa — Testes: ListaCompra · API
> Sprint 3 (05/08–19/08/2026) · Bloco: Compras · Item: ListaCompra · Passo 6/6 · Depende: Passos 2–5

## O que fazer
Fechar a cobertura automatizada do ListaCompra (repository, service, controller).

## Passo a passo
1. `ListaCompraRepositoryTest` (`@DataJpaTest`): persistência e queries.
2. `ListaCompraServiceTest` (Mockito): totais derivados, filtro por status.
3. `ListaCompraControllerIntegrationTest` (`MockMvc`): CRUD + erros.

## Onde mexer
- `src/test/java/br/com/contasdomesticas/api/**/ListaCompra*Test.java`

## Critério de pronto (DoD)
- [ ] `mvn verify` (profile test, H2) verde
- [ ] Cenários de erro cobertos (404/409/400)

## Como testar
`mvn verify` com Maven local + truststore Norton.
