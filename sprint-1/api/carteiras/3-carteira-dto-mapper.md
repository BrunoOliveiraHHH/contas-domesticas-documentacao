# Tarefa — DTO + Mapper: Carteira · API
> Sprint 1 (06/07–20/07/2026) · Bloco: Carteiras · Item: Carteira · Passo 3/6 · Depende: Passo 2 (entidade)

## O que fazer
Criar os DTOs (request/response) e o mapper MapStruct, com validação Bean Validation.

## Passo a passo
1. `dto/CarteiraRequest.java` (record) com `@NotBlank/@NotNull/@Size` nos campos obrigatórios.
2. `dto/CarteiraResponse.java` (record) sem dados sensíveis.
3. `mapper/CarteiraMapper.java` (`@Mapper(componentModel="spring")`): `toEntity`, `toResponse`.

## Onde mexer
- `br.com.contasdomesticas.api.dto.CarteiraRequest` / `CarteiraResponse`
- `br.com.contasdomesticas.api.mapper.CarteiraMapper`

## Critério de pronto (DoD)
- [ ] Validação rejeita payload inválido (400)
- [ ] Mapper converte entity ↔ dto corretamente

## Como testar
Coberto no teste de controller (payload inválido → 400 com `erros`).
