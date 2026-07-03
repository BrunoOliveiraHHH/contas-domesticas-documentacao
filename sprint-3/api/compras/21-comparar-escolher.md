# Tarefa — Comparar e escolher estabelecimento · API
> Sprint 3 (05/08–19/08/2026) · Bloco: Compras · Item Escolha · Depende: cotação de produto

## O que fazer
Indicar o menor preço do produto e escolher onde comprar cada item da lista.

## Passo a passo
1. Serviço que retorna a cotação mais barata do produto (normalizada por `fator_para_base`).
2. `PUT /api/v1/itens/{id}/escolha` grava `mercado_escolhido_id` e copia o preço da cotação escolhida (snapshot no item).

## Onde mexer
- `.../service/CotacaoProdutoService` (menor preço), `.../controller` (escolha)

## Critério de pronto (DoD)
- [ ] Menor preço destacado; escolher grava o estabelecimento e o preço no item

## Como testar
`CotacaoProdutoServiceTest`: menor preço; escolha atualiza o item.
