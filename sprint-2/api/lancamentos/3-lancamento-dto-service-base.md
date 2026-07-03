# Tarefa — DTO + Service base (validações) · API
> Sprint 2 (21/07–04/08/2026) · Bloco: Lançamentos · Item Lançamento base · Passo 3 · Depende: entidade Lancamento

## O que fazer
Criar DTOs comuns e o service base com validações compartilhadas.

## Passo a passo
1. DTOs base (request/response) + mapper.
2. Validações: valor maior que 0, `data_competencia` obrigatória, FKs válidas.
3. Métodos utilitários de consulta (período/carteira/tipo).

## Onde mexer
- `.../dto/Lancamento*`, `.../mapper/LancamentoMapper`, `.../service/LancamentoService`

## Critério de pronto (DoD)
- [ ] Valor menor/igual a 0 ou data ausente = 400

## Como testar
`LancamentoServiceTest`: validações.
