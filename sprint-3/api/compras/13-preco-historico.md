# Tarefa — Histórico de preço (gatilho + consulta) · API
> Sprint 3 (05/08–19/08/2026) · Bloco: Compras · Item Histórico de preço · Depende: ItemCompra, Mercado, Unidade

## O que fazer
Registrar o preço ao marcar item como comprado e expor a consulta com menor preço por unidade base.

## Passo a passo
1. Migração `V17` da tabela `preco_historico` (produto_normalizado, mercado_id, unidade_medida_id, preco_unitario, data); espelhar no db.
2. Ao marcar item comprado, gravar um `PrecoHistorico`.
3. `GET /api/v1/precos?produto=&mercado=` com normalização por `fator_para_base`.

## Onde mexer
- `.../db/migration/V17__*.sql`, `.../domain/PrecoHistorico`, `.../service/PrecoService`

## Critério de pronto (DoD)
- [ ] Comprar item alimenta o histórico
- [ ] Consulta retorna evolução e menor preço por unidade base

## Como testar
`PrecoServiceTest`: normalização e menor preço.
