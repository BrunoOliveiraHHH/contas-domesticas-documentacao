# Tarefa — Room: Forma de Pagamento (entity + DAO) · App
> Sprint 1 (06/07–20/07/2026) · Bloco: Cadastros · Item: Forma de Pagamento · Passo 1/4 · Depende: base do app

## O que fazer
Espelhar Forma de Pagamento no banco local (Room).

## Passo a passo
1. Criar `data/local/entity/FormaPagamentoEntity.kt` (`@Entity("forma_pagamento")`) com: nome, tipo, carteiraVinculada, diaFechamento, diaVencimento, ativa.
2. Criar `data/local/dao/FormaPagamentoDao.kt` (insert/update/delete/getAll Flow/getById).
3. Registrar em `AppDatabase` (nova entidade + bump da `version` + migração).

## Onde mexer
- `data/local/entity/FormaPagamentoEntity.kt`, `data/local/dao/FormaPagamentoDao.kt`, `data/local/AppDatabase.kt`

## Critério de pronto (DoD)
- [ ] Entidade e DAO compilam; AppDatabase migra sem erro

## Como testar
Verificação estática + build no Android Studio (futuro teste instrumentado de DAO).
