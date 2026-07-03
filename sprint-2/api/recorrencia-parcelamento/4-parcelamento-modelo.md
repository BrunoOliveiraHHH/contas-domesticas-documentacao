# Tarefa — Modelo de parcela (migração + entidade) · API
> Sprint 2 (21/07–04/08/2026) · Bloco: Recorrência & Parcelamento · Item Parcelamento · Passo 1 · Depende: Despesa, Forma de Pagamento

## O que fazer
Modelar o parcelamento (compra no crédito).

## Passo a passo
1. Decidir: tabela `parcela` (`V13`) OU N lançamentos ligados por `grupo_parcela` (uuid).
2. Se tabela: migração `V13__cria_tabela_parcela.sql` + entidade + repositório; espelhar no db.

## Onde mexer
- `.../db/migration/V13__*.sql`, `.../domain/Parcela` (se adotada)

## Critério de pronto (DoD)
- [ ] Modelo escolhido criado e migrado

## Como testar
Subir em dev (se tabela).
