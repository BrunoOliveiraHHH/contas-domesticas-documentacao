# Tarefa — Testes: FormaPagamento · API
> Sprint 1 (06/07–20/07/2026) · Bloco: Cadastros · Item: FormaPagamento · Passo 6/6 · Depende: Passos 2–5

## O que fazer
Fechar a cobertura automatizada do FormaPagamento (repository, service, controller).

## Passo a passo
1. `FormaPagamentoRepositoryTest` (`@DataJpaTest`): persistência e queries.
2. `FormaPagamentoServiceTest` (Mockito): validação condicional dos dias no crédito.
3. `FormaPagamentoControllerIntegrationTest` (`MockMvc`): CRUD + erros.

## Onde mexer
- `src/test/java/br/com/contasdomesticas/api/**/FormaPagamento*Test.java`

## Critério de pronto (DoD)
- [ ] `mvn verify` (profile test, H2) verde
- [ ] Cenários de erro cobertos (404/409/400)

## Como testar
`mvn verify` com Maven local + truststore Norton.
