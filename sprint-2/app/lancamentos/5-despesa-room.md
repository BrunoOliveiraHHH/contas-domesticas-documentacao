# Tarefa — Room: Despesa (entity + DAO) · App
> Sprint 2 (21/07–04/08/2026) · Bloco: Lançamentos · Item: Despesa · Passo 1/4 · Depende: base do app

## O que fazer
Espelhar Despesa no banco local (Room).

## Passo a passo
1. Criar `data/local/entity/DespesaEntity.kt` (`@Entity("despesa")`) com: valor, vencimento, status, carteira, categoria, formaPagamento.
2. Criar `data/local/dao/DespesaDao.kt` (insert/update/delete/getAll Flow/getById).
3. Registrar em `AppDatabase` (nova entidade + bump da `version` + migração).

## Onde mexer
- `data/local/entity/DespesaEntity.kt`, `data/local/dao/DespesaDao.kt`, `data/local/AppDatabase.kt`

## Critério de pronto (DoD)
- [ ] Entidade e DAO compilam; AppDatabase migra sem erro

## Como testar
Verificação estática + build no Android Studio (futuro teste instrumentado de DAO).
