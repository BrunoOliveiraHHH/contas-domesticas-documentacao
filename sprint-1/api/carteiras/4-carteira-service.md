# Tarefa — Service (regras): Carteira · API
> Sprint 1 (06/07–20/07/2026) · Bloco: Carteiras · Item: Carteira · Passo 4/6 · Depende: Passos 2 e 3

## O que fazer
Criar o service com o CRUD e as regras de negócio do Carteira.

## Passo a passo
1. `service/CarteiraService.java` (`@Service`, `@RequiredArgsConstructor`): listar, buscarPorId, criar, atualizar, remover.
2. Regras específicas: carteira INDIVIDUAL só visível ao dono; FAMILIAR compartilhada; não remover carteira com lançamentos; saldo atual é derivado (não persiste).
3. Lançar `AplicacaoException(mensagem, HttpStatus)` nos erros (404, 409, 400 conforme o caso).

## Onde mexer
- `br.com.contasdomesticas.api.service.CarteiraService`

## Critério de pronto (DoD)
- [ ] CRUD funciona; regras aplicadas
- [ ] Erros usam `AplicacaoException` (ProblemDetail)

## Como testar
`CarteiraServiceTest` (Mockito): regra de visibilidade por dono, bloqueio de remoção com lançamentos, exigir dono quando INDIVIDUAL.
