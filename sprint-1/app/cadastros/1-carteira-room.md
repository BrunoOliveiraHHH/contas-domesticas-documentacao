# Tarefa — Room: Carteira (entity + DAO) · App
> Sprint 1 (06/07–20/07/2026) · Bloco: Cadastros · Item: Carteira · Passo 1/4 · Depende: base do app

## O que fazer
Espelhar Carteira no banco local (Room).

## Passo a passo
1. Criar `data/local/entity/CarteiraEntity.kt` (`@Entity("carteira")`) com: nome, tipo, dono, saldoInicial, moeda, cor, icone, ativa.
2. Criar `data/local/dao/CarteiraDao.kt` (insert/update/delete/getAll Flow/getById).
3. Registrar em `AppDatabase` (nova entidade + bump da `version` + migração).

## Onde mexer
- `data/local/entity/CarteiraEntity.kt`, `data/local/dao/CarteiraDao.kt`, `data/local/AppDatabase.kt`

## Critério de pronto (DoD)
- [ ] Entidade e DAO compilam; AppDatabase migra sem erro

## Como testar
Verificação estática + build no Android Studio (futuro teste instrumentado de DAO).
