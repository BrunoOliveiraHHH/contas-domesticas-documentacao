# Tarefa — DTO + Mapper: Parametro · API
> Sprint 2 (21/07–04/08/2026) · Bloco: Parâmetros & Configuração · Item: Parametro · Passo 3/6 · Depende: Passo 2 (entidade)

## O que fazer
Criar os DTOs (request/response) e o mapper MapStruct, com validação Bean Validation.

## Passo a passo
1. `dto/ParametroRequest.java` (record) com `@NotBlank/@NotNull/@Size` nos campos obrigatórios.
2. `dto/ParametroResponse.java` (record) sem dados sensíveis.
3. `mapper/ParametroMapper.java` (`@Mapper(componentModel="spring")`): `toEntity`, `toResponse`.

## Onde mexer
- `br.com.contasdomesticas.api.dto.ParametroRequest` / `ParametroResponse`
- `br.com.contasdomesticas.api.mapper.ParametroMapper`

## Critério de pronto (DoD)
- [ ] Validação rejeita payload inválido (400)
- [ ] Mapper converte entity ↔ dto corretamente

## Como testar
Coberto no teste de controller (payload inválido → 400 com `erros`).
