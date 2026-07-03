# Tarefa — Histórico de listas (inclui não fechadas) · API
> Sprint 3 (05/08–19/08/2026) · Bloco: Compras · Item Histórico de listas · Depende: ListaCompra

## O que fazer
Listar as listas do usuário, inclusive as não fechadas (para reutilização).

## Passo a passo
1. `GET /api/v1/listas-compra?status=` retorna ABERTA/FECHADA/ARQUIVADA.
2. Permitir `ARQUIVADA` (não virou despesa, mas fica guardada).

## Onde mexer
- `.../controller/ListaCompraController`, `.../service`

## Critério de pronto (DoD)
- [ ] Listas não fechadas permanecem acessíveis no histórico

## Como testar
`ListaCompraControllerIntegrationTest`: filtro por status.
