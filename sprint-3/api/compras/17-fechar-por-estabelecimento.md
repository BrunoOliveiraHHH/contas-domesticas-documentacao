# Tarefa — Fechar lista → despesa por estabelecimento · API
> Sprint 3 (05/08–19/08/2026) · Bloco: Compras · Item Fechar · Depende: ItemCompra, escolha, Despesa

## O que fazer
Ao fechar, agrupar os itens pelo estabelecimento escolhido e gerar uma despesa por estabelecimento.

## Passo a passo
1. `POST /api/v1/listas-compra/{id}/fechar`: agrupa itens por `mercado_escolhido`; para cada grupo cria um `Lancamento` DESPESA (total do estabelecimento).
2. Vincular as despesas à lista (1-N — decidir: `lancamento.lista_compra_id` ou tabela de ligação).
3. Marca a lista como `FECHADA`; grava o `preco_historico` dos itens.
4. Idempotente: lista já fechada não gera novas despesas.

## Onde mexer
- `.../service/ListaCompraService` (fechar), `.../controller/ListaCompraController`

## Critério de pronto (DoD)
- [ ] Fechar gera 1 despesa por estabelecimento escolhido; refechar não duplica

## Como testar
`ListaCompraServiceTest.deveFecharGerandoDespesaPorEstabelecimento`.
