# Tarefa — Migração Flyway: tabela `item_compra` · API
> Sprint 3 (05/08–19/08/2026) · Bloco: Compras · Item: ItemCompra · Passo 1/6 · Depende: base do projeto

## O que fazer
Criar a migração Flyway **V16** que cria a tabela `item_compra` e espelhar os scripts no repo `contas-domesticas-db`.

## Passo a passo
1. Criar `src/main/resources/db/migration/V16__cria_tabela_item_compra.sql`.
2. Colunas: id `bigint generated always as identity` + lista_compra_id (FK), produto, categoria_id opcional, quantidade numeric(12,3), unidade_medida_id, preco_unitario_estimado, preco_unitario_real, comprado boolean, mercado_id override + auditoria (`criado_em`, `criado_por`, `atualizado_em`, `atualizado_por`).
3. Adicionar PK (`pk_item_compra`) e índices/único necessários.
4. Espelhar em `contas-domesticas-db/ddl/{tables,primary,index}/item_compra.sql`.

## Onde mexer
- `contas-domesticas-api/src/main/resources/db/migration/V16__cria_tabela_item_compra.sql`
- `contas-domesticas-db/ddl/{tables,primary,index}/item_compra.sql`

## Critério de pronto (DoD)
- [ ] App sobe em `dev` e o Flyway aplica V16 sem erro
- [ ] Scripts espelhados no repo db

## Como testar
Subir no profile `dev` (Flyway aplica) ou rodar o teste de contexto; conferir tipos/constraints.
