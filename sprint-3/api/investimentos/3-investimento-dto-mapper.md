# Tarefa — DTO + Mapper: Investimento · API
> Sprint 3 (05/08–19/08/2026) · Bloco: Investimentos · Item: Investimento · Passo 3/6 · Depende: Passo 2 (entidade)

## O que fazer
Criar os DTOs (request/response) e o mapper MapStruct, com validação Bean Validation.

## Passo a passo
1. `dto/InvestimentoRequest.java` (record) com `@NotBlank/@NotNull/@Size` nos campos obrigatórios.
2. `dto/InvestimentoResponse.java` (record) sem dados sensíveis.
3. `mapper/InvestimentoMapper.java` (`@Mapper(componentModel="spring")`): `toEntity`, `toResponse`.

## Onde mexer
- `br.com.contasdomesticas.api.dto.InvestimentoRequest` / `InvestimentoResponse`
- `br.com.contasdomesticas.api.mapper.InvestimentoMapper`

## Critério de pronto (DoD)
- [ ] Validação rejeita payload inválido (400)
- [ ] Mapper converte entity ↔ dto corretamente

## Como testar
Coberto no teste de controller (payload inválido → 400 com `erros`).
