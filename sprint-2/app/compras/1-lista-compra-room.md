# Tarefa — Room: Lista de Compra (entity + DAO) · App
> Sprint 2 (21/07–04/08/2026) · Bloco: Compras · Item: Lista de Compra · Passo 1/4 · Depende: base do app

## O que fazer
Espelhar Lista de Compra no banco local (Room).

## Passo a passo
1. `data/local/entity/ListaCompraEntity.kt` (`@Entity("lista_compra")`) com: nome, tipo, carteira, data, status (ABERTA/FECHADA/ARQUIVADA).
2. `data/local/dao/ListaCompraDao.kt` (insert/update/delete/getAll Flow/getById).
3. Registrar em `AppDatabase` (bump da `version` + migração).

## Onde mexer
- `data/local/entity/ListaCompraEntity.kt`, `data/local/dao/ListaCompraDao.kt`, `data/local/AppDatabase.kt`

## Critério de pronto (DoD)
- [ ] Entidade e DAO compilam; AppDatabase migra

## Como testar
Verificação estática + build no Android Studio.
