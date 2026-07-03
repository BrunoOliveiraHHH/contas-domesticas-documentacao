# Tarefa — Service (regras): Parametro · API
> Sprint 2 (21/07–04/08/2026) · Bloco: Parâmetros & Configuração · Item: Parametro · Passo 4/6 · Depende: Passos 2 e 3

## O que fazer
Criar o service com o CRUD e as regras de negócio do Parametro.

## Passo a passo
1. `service/ParametroService.java` (`@Service`, `@RequiredArgsConstructor`): listar, buscarPorId, criar, atualizar, remover.
2. Regras específicas: retornar o valor vigente na data consultada; manter histórico por vigência.
3. Lançar `AplicacaoException(mensagem, HttpStatus)` nos erros (404, 409, 400 conforme o caso).

## Onde mexer
- `br.com.contasdomesticas.api.service.ParametroService`

## Critério de pronto (DoD)
- [ ] CRUD funciona; regras aplicadas
- [ ] Erros usam `AplicacaoException` (ProblemDetail)

## Como testar
`ParametroServiceTest` (Mockito): seleção do valor vigente por data.
