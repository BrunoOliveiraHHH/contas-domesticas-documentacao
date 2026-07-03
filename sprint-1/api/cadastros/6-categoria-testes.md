# Tarefa — Testes: Categoria · API
> Sprint 1 (06/07–20/07/2026) · Bloco: Cadastros · Item: Categoria · Passo 6/6 · Depende: Passos 2–5

## O que fazer
Fechar a cobertura automatizada do Categoria (repository, service, controller).

## Passo a passo
1. `CategoriaRepositoryTest` (`@DataJpaTest`): persistência e queries.
2. `CategoriaServiceTest` (Mockito): herança de tipo, anti-ciclo, montagem da árvore.
3. `CategoriaControllerIntegrationTest` (`MockMvc`): CRUD + erros.

## Onde mexer
- `src/test/java/br/com/contasdomesticas/api/**/Categoria*Test.java`

## Critério de pronto (DoD)
- [ ] `mvn verify` (profile test, H2) verde
- [ ] Cenários de erro cobertos (404/409/400)

## Como testar
`mvn verify` com Maven local + truststore Norton.
