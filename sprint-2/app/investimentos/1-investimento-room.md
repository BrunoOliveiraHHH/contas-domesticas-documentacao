# Tarefa — Room: Investimento (entity + DAO) · App
> Sprint 2 (21/07–04/08/2026) · Bloco: Investimentos · Item: Investimento · Passo 1/4 · Depende: base do app

## O que fazer
Espelhar Investimento no banco local (Room).

## Passo a passo
1. Criar `data/local/entity/InvestimentoEntity.kt` (`@Entity("investimento")`) com: nome, tipo, instituicao, indexador, taxa, datas; aportes/resgates.
2. Criar `data/local/dao/InvestimentoDao.kt` (insert/update/delete/getAll Flow/getById).
3. Registrar em `AppDatabase` (nova entidade + bump da `version` + migração).

## Onde mexer
- `data/local/entity/InvestimentoEntity.kt`, `data/local/dao/InvestimentoDao.kt`, `data/local/AppDatabase.kt`

## Critério de pronto (DoD)
- [ ] Entidade e DAO compilam; AppDatabase migra sem erro

## Como testar
Verificação estática + build no Android Studio (futuro teste instrumentado de DAO).
