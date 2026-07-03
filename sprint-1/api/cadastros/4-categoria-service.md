# Tarefa — Service (regras): Categoria · API
> Sprint 1 (06/07–20/07/2026) · Bloco: Cadastros · Item: Categoria · Passo 4/6 · Depende: Passos 2 e 3

## O que fazer
Criar o service com o CRUD e as regras de negócio do Categoria.

## Passo a passo
1. `service/CategoriaService.java` (`@Service`, `@RequiredArgsConstructor`): listar, buscarPorId, criar, atualizar, remover.
2. Regras específicas: subcategoria herda o tipo da pai; impedir ciclo (pai não pode ser descendente); endpoint de árvore.
3. Lançar `AplicacaoException(mensagem, HttpStatus)` nos erros (404, 409, 400 conforme o caso).

## Onde mexer
- `br.com.contasdomesticas.api.service.CategoriaService`

## Critério de pronto (DoD)
- [ ] CRUD funciona; regras aplicadas
- [ ] Erros usam `AplicacaoException` (ProblemDetail)

## Como testar
`CategoriaServiceTest` (Mockito): herança de tipo, anti-ciclo, montagem da árvore.
