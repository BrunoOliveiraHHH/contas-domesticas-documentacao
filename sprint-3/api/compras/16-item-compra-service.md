# Tarefa — Service (regras): ItemCompra · API
> Sprint 3 (05/08–19/08/2026) · Bloco: Compras · Item: ItemCompra · Passo 4/6 · Depende: Passos 2 e 3

## O que fazer
Criar o service com o CRUD e as regras de negócio do ItemCompra.

## Passo a passo
1. `service/ItemCompraService.java` (`@Service`, `@RequiredArgsConstructor`): listar, buscarPorId, criar, atualizar, remover.
2. Regras específicas: o item referencia um produto do catálogo; o preço vem da cotação do produto no estabelecimento escolhido; marcar comprado exige escolha.
3. Lançar `AplicacaoException(mensagem, HttpStatus)` nos erros (404, 409, 400 conforme o caso).

## Onde mexer
- `br.com.contasdomesticas.api.service.ItemCompraService`

## Critério de pronto (DoD)
- [ ] CRUD funciona; regras aplicadas
- [ ] Erros usam `AplicacaoException` (ProblemDetail)

## Como testar
`ItemCompraServiceTest` (Mockito): referência ao catálogo; preço do estabelecimento escolhido; regra de comprado.
