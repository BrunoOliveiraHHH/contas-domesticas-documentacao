# Tarefa — Cotação de Produto: registrar e listar · API
> Sprint 3 (05/08–19/08/2026) · Bloco: Compras · Item Cotação · Passo 2 · Depende: cotacao-produto-modelo

## O que fazer
Registrar/consultar os preços de um produto por estabelecimento (catálogo de preços).

## Passo a passo
1. `POST /api/v1/produtos/{id}/cotacoes` (mercado + preço unitário).
2. `GET /api/v1/produtos/{id}/cotacoes` (lista ordenada por preço por unidade base).

## Onde mexer
- `.../controller/CotacaoProdutoController`, `.../service/CotacaoProdutoService`

## Critério de pronto (DoD)
- [ ] Registrar e listar cotações do produto; reaproveitáveis em qualquer lista

## Como testar
`CotacaoProdutoControllerIntegrationTest`.
