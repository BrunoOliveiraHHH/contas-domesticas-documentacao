# Tarefa — Cotação: migração + entidade · API
> Sprint 3 (05/08–19/08/2026) · Bloco: Compras · Item Cotação · Passo 1 · Depende: ItemCompra, Mercado

## O que fazer
Modelar as cotações de preço de um item por estabelecimento (para comparar antes de comprar).

## Passo a passo
1. Migração `V21` da tabela `cotacao_item` (item_compra_id, mercado_id, preco_unitario, data); espelhar no db.
2. `domain/CotacaoItem` (estende `BaseEntity`) + repositório.

## Onde mexer
- `.../db/migration/V21__cria_tabela_cotacao_item.sql`, `.../domain/CotacaoItem`

## Critério de pronto (DoD)
- [ ] Flyway aplica V21; um item pode ter várias cotações (uma por estabelecimento)

## Como testar
`CotacaoRepositoryTest`: várias cotações por item.
