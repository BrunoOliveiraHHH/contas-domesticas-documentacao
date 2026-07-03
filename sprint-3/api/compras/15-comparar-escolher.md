# Tarefa — Comparar e escolher estabelecimento · API
> Sprint 3 (05/08–19/08/2026) · Bloco: Compras · Item Escolha · Depende: cotacao-endpoints

## O que fazer
Indicar o menor preço e permitir escolher onde comprar cada item.

## Passo a passo
1. Serviço que retorna a cotação mais barata (normalizada por `fator_para_base`).
2. `PUT /api/v1/itens/{id}/escolha` grava `mercado_escolhido_id` e copia o preço da cotação escolhida.

## Onde mexer
- `.../service/CotacaoService` (menor preço), `.../controller` (escolha)

## Critério de pronto (DoD)
- [ ] Menor preço destacado; escolher grava o estabelecimento e o preço no item

## Como testar
`CotacaoServiceTest`: menor preço; escolha atualiza o item.
