# Tarefa — Service (regras): Preferencia · API
> Sprint 2 (21/07–04/08/2026) · Bloco: Parâmetros & Configuração · Item: Preferencia · Passo 4/6 · Depende: Passos 2 e 3

## O que fazer
Criar o service com o CRUD e as regras de negócio do Preferencia.

## Passo a passo
1. `service/PreferenciaService.java` (`@Service`, `@RequiredArgsConstructor`): listar, buscarPorId, criar, atualizar, remover.
2. Regras específicas: resolução usuário para global para default.
3. Lançar `AplicacaoException(mensagem, HttpStatus)` nos erros (404, 409, 400 conforme o caso).

## Onde mexer
- `br.com.contasdomesticas.api.service.PreferenciaService`

## Critério de pronto (DoD)
- [ ] CRUD funciona; regras aplicadas
- [ ] Erros usam `AplicacaoException` (ProblemDetail)

## Como testar
`PreferenciaServiceTest` (Mockito): fallback global e default.
