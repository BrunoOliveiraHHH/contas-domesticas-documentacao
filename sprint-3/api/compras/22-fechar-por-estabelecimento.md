# Tarefa — Fechar lista → despesa por estabelecimento · API
> Sprint 3 (05/08–19/08/2026) · Bloco: Compras · Item Fechar · Depende: item, escolha, Despesa

## O que fazer
Ao fechar, agrupar os itens pelo estabelecimento escolhido e gerar uma despesa por estabelecimento.

## Passo a passo
1. `POST /api/v1/listas-compra/{id}/fechar`: agrupa itens por `mercado_escolhido`; cria um `Lancamento` DESPESA por grupo (total do estabelecimento).
2. Vincular as despesas à lista (1-N — `lancamento.lista_compra_id` ou tabela de ligação; decidir na análise).
3. Marca a lista `FECHADA`; grava no catálogo uma `cotacao_produto` `origem=COMPRA` (preço realizado).
4. Idempotente: lista já fechada não gera novas despesas.

## Onde mexer
- `.../service/ListaCompraService` (fechar), `.../controller/ListaCompraController`

## Critério de pronto (DoD)
- [ ] Fechar gera 1 despesa por estabelecimento; refechar não duplica; catálogo recebe o preço pago

## Como testar
`ListaCompraServiceTest.deveFecharGerandoDespesaPorEstabelecimento`.
