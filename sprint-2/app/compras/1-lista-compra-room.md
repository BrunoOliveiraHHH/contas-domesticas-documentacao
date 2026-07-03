# Tarefa — Room: Lista de Compra (entity + DAO) · App
> Sprint 2 (21/07–04/08/2026) · Bloco: Compras · Item: Lista de Compra · Passo 1/4 · Depende: base do app

## O que fazer
Espelhar Lista de Compra no banco local (Room).

## Passo a passo
1. Criar `data/local/entity/ListaCompraEntity.kt` (`@Entity("lista_compra")`) com: nome, tipo, mercado, carteira, status.
2. Criar `data/local/dao/ListaCompraDao.kt` (insert/update/delete/getAll Flow/getById).
3. Registrar em `AppDatabase` (nova entidade + bump da `version` + migração).

## Onde mexer
- `data/local/entity/ListaCompraEntity.kt`, `data/local/dao/ListaCompraDao.kt`, `data/local/AppDatabase.kt`

## Critério de pronto (DoD)
- [ ] Entidade e DAO compilam; AppDatabase migra sem erro

## Como testar
Verificação estática + build no Android Studio (futuro teste instrumentado de DAO).
