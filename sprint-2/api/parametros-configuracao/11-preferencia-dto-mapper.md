# Tarefa — DTO + Mapper: Preferencia · API
> Sprint 2 (21/07–04/08/2026) · Bloco: Parâmetros & Configuração · Item: Preferencia · Passo 3/6 · Depende: Passo 2 (entidade)

## O que fazer
Criar os DTOs (request/response) e o mapper MapStruct, com validação Bean Validation.

## Passo a passo
1. `dto/PreferenciaRequest.java` (record) com `@NotBlank/@NotNull/@Size` nos campos obrigatórios.
2. `dto/PreferenciaResponse.java` (record) sem dados sensíveis.
3. `mapper/PreferenciaMapper.java` (`@Mapper(componentModel="spring")`): `toEntity`, `toResponse`.

## Onde mexer
- `br.com.contasdomesticas.api.dto.PreferenciaRequest` / `PreferenciaResponse`
- `br.com.contasdomesticas.api.mapper.PreferenciaMapper`

## Critério de pronto (DoD)
- [ ] Validação rejeita payload inválido (400)
- [ ] Mapper converte entity ↔ dto corretamente

## Como testar
Coberto no teste de controller (payload inválido → 400 com `erros`).
