# Tarefa — Service (regras): FormaPagamento · API
> Sprint 1 (06/07–20/07/2026) · Bloco: Cadastros · Item: FormaPagamento · Passo 4/6 · Depende: Passos 2 e 3

## O que fazer
Criar o service com o CRUD e as regras de negócio do FormaPagamento.

## Passo a passo
1. `service/FormaPagamentoService.java` (`@Service`, `@RequiredArgsConstructor`): listar, buscarPorId, criar, atualizar, remover.
2. Regras específicas: dias de fechamento/vencimento só válidos e exigidos quando tipo=CREDITO.
3. Lançar `AplicacaoException(mensagem, HttpStatus)` nos erros (404, 409, 400 conforme o caso).

## Onde mexer
- `br.com.contasdomesticas.api.service.FormaPagamentoService`

## Critério de pronto (DoD)
- [ ] CRUD funciona; regras aplicadas
- [ ] Erros usam `AplicacaoException` (ProblemDetail)

## Como testar
`FormaPagamentoServiceTest` (Mockito): validação condicional dos dias no crédito.
