# Tarefa — Relatório: gasto por categoria · API
> Sprint 3 (05/08–19/08/2026) · Bloco: Relatórios · Item Por categoria · Depende: Despesa, Categoria

## O que fazer
Expor `GET /api/v1/relatorios/por-categoria?periodo=&tipo=` com percentual do total.

## Passo a passo
1. Agregação hierárquica (categoria raiz + subcategorias); percentual do total.

## Onde mexer
- `.../service/RelatorioCategoriaService`, `.../controller/RelatorioController`

## Critério de pronto (DoD)
- [ ] Soma por categoria = total do período; drill-down por subcategoria

## Como testar
`RelatorioCategoriaServiceTest`.
