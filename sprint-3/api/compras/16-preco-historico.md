# Tarefa — Histórico de preço realizado · API
> Sprint 3 (05/08–19/08/2026) · Bloco: Compras · Item Histórico · Depende: ItemCompra, Mercado, Unidade

## O que fazer
Registrar o preço efetivamente pago (no fechamento) para tendência entre listas.

## Passo a passo
1. Migração `V17` da tabela `preco_historico` (produto_normalizado, mercado_id, unidade_medida_id, preco_unitario, data).
2. No fechamento, gravar `PrecoHistorico` do preço pago; `GET /api/v1/precos` para consultar a evolução.

## Onde mexer
- `.../db/migration/V17__*.sql`, `.../domain/PrecoHistorico`, `.../service/PrecoService`

## Critério de pronto (DoD)
- [ ] Fechamento alimenta o histórico; consulta retorna evolução por estabelecimento

## Como testar
`PrecoServiceTest`.
