# Tarefa — Cotação: registrar e listar preços por estabelecimento · API
> Sprint 3 (05/08–19/08/2026) · Bloco: Compras · Item Cotação · Passo 2 · Depende: cotacao-modelo

## O que fazer
Permitir registrar o preço de um item em cada estabelecimento e listar as cotações.

## Passo a passo
1. `POST /api/v1/itens/{id}/cotacoes` (mercado + preço unitário).
2. `GET /api/v1/itens/{id}/cotacoes` (lista ordenada por preço/unidade base).

## Onde mexer
- `.../controller/CotacaoController`, `.../service/CotacaoService`

## Critério de pronto (DoD)
- [ ] Registrar e listar cotações; ordenação por preço por unidade base

## Como testar
`CotacaoControllerIntegrationTest`.
