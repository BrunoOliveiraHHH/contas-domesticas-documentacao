# Tarefa — Service (regras): Produto · API
> Sprint 3 (05/08–19/08/2026) · Bloco: Compras · Item: Produto · Passo 4/6 · Depende: Passos 2 e 3

## O que fazer
Criar o service com o CRUD e as regras de negócio do Produto.

## Passo a passo
1. `service/ProdutoService.java` (`@Service`, `@RequiredArgsConstructor`): listar, buscarPorId, criar, atualizar, remover.
2. Regras específicas: catálogo reutilizável entre listas; o item de compra referencia um produto (não digita texto livre).
3. Lançar `AplicacaoException(mensagem, HttpStatus)` nos erros (404, 409, 400 conforme o caso).

## Onde mexer
- `br.com.contasdomesticas.api.service.ProdutoService`

## Critério de pronto (DoD)
- [ ] CRUD funciona; regras aplicadas
- [ ] Erros usam `AplicacaoException` (ProblemDetail)

## Como testar
`ProdutoServiceTest` (Mockito): CRUD; busca por nome/categoria; produto reaproveitado em várias listas.
