# Tarefa — Cotação de Produto: migração + entidade · API
> Sprint 3 (05/08–19/08/2026) · Bloco: Compras · Item Cotação (reutilizável) · Passo 1 · Depende: Produto, Mercado

## O que fazer
Modelar o preço de um produto por estabelecimento, **reutilizável em qualquer lista**.

## Passo a passo
1. Migração `V18` da tabela `cotacao_produto` (produto_id, mercado_id, preco_unitario, data, origem COTACAO/COMPRA); espelhar no db.
2. `domain/CotacaoProduto` (estende `BaseEntity`) + repositório (por produto, por produto+mercado).

## Onde mexer
- `.../db/migration/V18__cria_tabela_cotacao_produto.sql`, `.../domain/CotacaoProduto`

## Critério de pronto (DoD)
- [ ] Um produto pode ter várias cotações (uma por estabelecimento, com histórico por data)
- [ ] `origem` distingue cotação (planejada) de compra (realizada)

## Como testar
`CotacaoProdutoRepositoryTest`: várias cotações por produto/mercado.
