# Tarefa — Service (regras): Mercado · API
> Sprint 1 (06/07–20/07/2026) · Bloco: Cadastros · Item: Mercado · Passo 4/6 · Depende: Passos 2 e 3

## O que fazer
Criar o service com o CRUD e as regras de negócio do Mercado.

## Passo a passo
1. `service/MercadoService.java` (`@Service`, `@RequiredArgsConstructor`): listar, buscarPorId, criar, atualizar, remover.
2. Regras específicas: filtro por tipo.
3. Lançar `AplicacaoException(mensagem, HttpStatus)` nos erros (404, 409, 400 conforme o caso).

## Onde mexer
- `br.com.contasdomesticas.api.service.MercadoService`

## Critério de pronto (DoD)
- [ ] CRUD funciona; regras aplicadas
- [ ] Erros usam `AplicacaoException` (ProblemDetail)

## Como testar
`MercadoServiceTest` (Mockito): filtro por tipo, CRUD e 404.
