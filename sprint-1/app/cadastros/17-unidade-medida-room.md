# Tarefa — Room: Unidade de Medida (entity + DAO) · App
> Sprint 1 (06/07–20/07/2026) · Bloco: Cadastros · Item: Unidade de Medida · Passo 1/4 · Depende: base do app

## O que fazer
Espelhar Unidade de Medida no banco local (Room).

## Passo a passo
1. Criar `data/local/entity/UnidadeMedidaEntity.kt` (`@Entity("unidade_medida")`) com: nome, sigla, tipo, fatorParaBase.
2. Criar `data/local/dao/UnidadeMedidaDao.kt` (insert/update/delete/getAll Flow/getById).
3. Registrar em `AppDatabase` (nova entidade + bump da `version` + migração).

## Onde mexer
- `data/local/entity/UnidadeMedidaEntity.kt`, `data/local/dao/UnidadeMedidaDao.kt`, `data/local/AppDatabase.kt`

## Critério de pronto (DoD)
- [ ] Entidade e DAO compilam; AppDatabase migra sem erro

## Como testar
Verificação estática + build no Android Studio (futuro teste instrumentado de DAO).
