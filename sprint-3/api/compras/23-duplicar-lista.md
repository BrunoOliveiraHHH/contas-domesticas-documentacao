# Tarefa — Duplicar/reutilizar lista · API
> Sprint 3 (05/08–19/08/2026) · Bloco: Compras · Item Reutilização · Depende: ListaCompra

## O que fazer
Criar uma nova lista a partir de uma existente (reaproveitar itens/produtos).

## Passo a passo
1. `POST /api/v1/listas-compra/{id}/duplicar`: copia os itens (produto + quantidade), status `ABERTA`, sem escolha/preço fixado.

## Onde mexer
- `.../service/ListaCompraService` (duplicar)

## Critério de pronto (DoD)
- [ ] Nova lista ABERTA com os itens copiados; a original permanece intacta

## Como testar
`ListaCompraServiceTest.deveDuplicarLista`.
