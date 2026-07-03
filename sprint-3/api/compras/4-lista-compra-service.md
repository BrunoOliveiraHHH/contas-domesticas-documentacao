# Tarefa — Service (regras): ListaCompra · API
> Sprint 3 (05/08–19/08/2026) · Bloco: Compras · Item: ListaCompra · Passo 4/6 · Depende: Passos 2 e 3

## O que fazer
Criar o service com o CRUD e as regras de negócio do ListaCompra.

## Passo a passo
1. `service/ListaCompraService.java` (`@Service`, `@RequiredArgsConstructor`): listar, buscarPorId, criar, atualizar, remover.
2. Regras específicas: totais estimado/real derivados dos itens; filtro por status/tipo.
3. Lançar `AplicacaoException(mensagem, HttpStatus)` nos erros (404, 409, 400 conforme o caso).

## Onde mexer
- `br.com.contasdomesticas.api.service.ListaCompraService`

## Critério de pronto (DoD)
- [ ] CRUD funciona; regras aplicadas
- [ ] Erros usam `AplicacaoException` (ProblemDetail)

## Como testar
`ListaCompraServiceTest` (Mockito): totais derivados, filtro por status.
