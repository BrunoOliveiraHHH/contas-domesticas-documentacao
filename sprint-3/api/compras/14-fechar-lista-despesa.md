# Tarefa — Fechar lista gera 1 despesa · API
> Sprint 3 (05/08–19/08/2026) · Bloco: Compras · Item Fechar-despesa · Depende: ListaCompra, ItemCompra, Despesa

## O que fazer
Ao fechar a lista, criar uma despesa com o total real e vincular.

## Passo a passo
1. `POST /api/v1/listas-compra/{id}/fechar`: cria `Lancamento` DESPESA (valor = total real, categoria default por tipo), marca `status=FECHADA`, vincula `despesa_gerada_id`.
2. Idempotente: lista já fechada não gera outra despesa.

## Onde mexer
- `.../service/ListaCompraService` (fechar), `.../controller/ListaCompraController`

## Critério de pronto (DoD)
- [ ] Fechar gera 1 despesa com o total; refechar não duplica

## Como testar
`ListaCompraServiceTest.deveFecharGerandoDespesa` (idempotente).
