# Tarefa — Duplicar/reutilizar lista · API
> Sprint 3 (05/08–19/08/2026) · Bloco: Compras · Item Reutilização · Depende: ListaCompra

## O que fazer
Permitir criar uma nova lista a partir de uma existente (reaproveitar itens).

## Passo a passo
1. `POST /api/v1/listas-compra/{id}/duplicar`: copia itens (produto/quantidade/unidade), status `ABERTA`, sem cotações/escolhas/preços.

## Onde mexer
- `.../service/ListaCompraService` (duplicar)

## Critério de pronto (DoD)
- [ ] Nova lista ABERTA com os itens copiados; a original permanece intacta

## Como testar
`ListaCompraServiceTest.deveDuplicarLista`.
