# Tarefa — Colunas de sincronização (V21) · DB
> Sprint 2 (21/07–04/08/2026) · Bloco: Sincronização · Item Sincronização · Depende: todas as tabelas de domínio

## O que fazer
Adicionar as colunas de sincronização às tabelas de domínio (espelho do Flyway V21 da API).

## Passo a passo
1. Em cada tabela sincronizável, adicionar: `uuid uuid`, `versao bigint default 0`, `atualizado_em timestamptz`, `deletado boolean default false`.
2. Índices: `ix_<tabela>_atualizado_em`; único `uk_<tabela>_uuid`.
3. Tabelas: carteira, categoria, forma_pagamento, mercado, unidade_medida, parametro, preferencia, lancamento, recorrencia, parcela, rateio, participante_rateio, lista_compra, item_compra, investimento, aporte, posicao_investimento.

## Onde mexer
- `contas-domesticas-db/ddl/` (alter das tabelas) — espelho do `V21` da API

## Critério de pronto (DoD)
- [ ] Todas as tabelas de domínio com uuid/versao/atualizado_em/deletado
- [ ] Índices de sincronização criados

## Como testar
Conferir contra a migração `V21` da API; rodar em banco limpo.
