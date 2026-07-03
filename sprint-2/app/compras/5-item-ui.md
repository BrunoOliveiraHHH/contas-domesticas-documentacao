# Tarefa — Item de compra (unidade/preço) · App
> Sprint 2 (21/07–04/08/2026) · Bloco: Compras · Item Item · Depende: lista, unidade, API item

## O que fazer
Adicionar/editar itens com quantidade, unidade e preço.

## Passo a passo
1. `ItemCompraEntity` + DAO; API + repositório.
2. Tela de item (produto, categoria, quantidade, unidade, preço estimado/real, comprado).
3. Total = qtd x preço; marcar comprado pede preço real.

## Onde mexer
- `data/local/.../ItemCompra*`, `ui/compras/*`

## Critério de pronto (DoD)
- [ ] Itens com cálculo de total; marcar comprado atualiza o total real

## Como testar
Verificação estática + build no Android Studio.
