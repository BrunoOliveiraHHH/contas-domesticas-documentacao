# Tarefa — Room: Produto (catálogo) (entity + DAO) · App
> Sprint 2 (21/07–04/08/2026) · Bloco: Compras · Item: Produto (catálogo) · Passo 1/4 · Depende: base do app

## O que fazer
Espelhar Produto (catálogo) no banco local (Room).

## Passo a passo
1. `data/local/entity/ProdutoEntity.kt` (`@Entity("produto")`) com: nome, descricao, categoria, unidadePadrao, codigoBarras, ativo.
2. `data/local/dao/ProdutoDao.kt` (insert/update/delete/getAll Flow/getById).
3. Registrar em `AppDatabase` (bump da `version` + migração).

## Onde mexer
- `data/local/entity/ProdutoEntity.kt`, `data/local/dao/ProdutoDao.kt`, `data/local/AppDatabase.kt`

## Critério de pronto (DoD)
- [ ] Entidade e DAO compilam; AppDatabase migra

## Como testar
Verificação estática + build no Android Studio.
