# Tarefa — DTO + Mapper: FormaPagamento · API
> Sprint 1 (06/07–20/07/2026) · Bloco: Cadastros · Item: FormaPagamento · Passo 3/6 · Depende: Passo 2 (entidade)

## O que fazer
Criar os DTOs (request/response) e o mapper MapStruct, com validação Bean Validation.

## Passo a passo
1. `dto/FormaPagamentoRequest.java` (record) com `@NotBlank/@NotNull/@Size` nos campos obrigatórios.
2. `dto/FormaPagamentoResponse.java` (record) sem dados sensíveis.
3. `mapper/FormaPagamentoMapper.java` (`@Mapper(componentModel="spring")`): `toEntity`, `toResponse`.

## Onde mexer
- `br.com.contasdomesticas.api.dto.FormaPagamentoRequest` / `FormaPagamentoResponse`
- `br.com.contasdomesticas.api.mapper.FormaPagamentoMapper`

## Critério de pronto (DoD)
- [ ] Validação rejeita payload inválido (400)
- [ ] Mapper converte entity ↔ dto corretamente

## Como testar
Coberto no teste de controller (payload inválido → 400 com `erros`).
