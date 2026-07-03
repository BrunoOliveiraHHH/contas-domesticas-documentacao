# Tarefa — Service (regras): Investimento · API
> Sprint 3 (05/08–19/08/2026) · Bloco: Investimentos · Item: Investimento · Passo 4/6 · Depende: Passos 2 e 3

## O que fazer
Criar o service com o CRUD e as regras de negócio do Investimento.

## Passo a passo
1. `service/InvestimentoService.java` (`@Service`, `@RequiredArgsConstructor`): listar, buscarPorId, criar, atualizar, remover.
2. Regras específicas: vincula à carteira (escopo).
3. Lançar `AplicacaoException(mensagem, HttpStatus)` nos erros (404, 409, 400 conforme o caso).

## Onde mexer
- `br.com.contasdomesticas.api.service.InvestimentoService`

## Critério de pronto (DoD)
- [ ] CRUD funciona; regras aplicadas
- [ ] Erros usam `AplicacaoException` (ProblemDetail)

## Como testar
`InvestimentoServiceTest` (Mockito): CRUD e busca por carteira.
