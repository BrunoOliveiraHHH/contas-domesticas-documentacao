# Tarefa — Migração Flyway: tabela `carteira` · API
> Sprint 1 (06/07–20/07/2026) · Bloco: Carteiras · Item: Carteira · Passo 1/6 · Depende: base do projeto

## O que fazer
Criar a migração Flyway **V4** que cria a tabela `carteira` e espelhar os scripts no repo `contas-domesticas-db`.

## Passo a passo
1. Criar `src/main/resources/db/migration/V4__cria_tabela_carteira.sql`.
2. Colunas: id `bigint generated always as identity` + nome, tipo (FAMILIAR/INDIVIDUAL), dono_id (nulo se familiar), saldo_inicial numeric(15,2), moeda varchar(3) default 'BRL', cor, icone, ativa boolean + auditoria (`criado_em`, `criado_por`, `atualizado_em`, `atualizado_por`).
3. Adicionar PK (`pk_carteira`) e índices/único necessários.
4. Espelhar em `contas-domesticas-db/ddl/{tables,primary,index}/carteira.sql`.

## Onde mexer
- `contas-domesticas-api/src/main/resources/db/migration/V4__cria_tabela_carteira.sql`
- `contas-domesticas-db/ddl/{tables,primary,index}/carteira.sql`

## Critério de pronto (DoD)
- [ ] App sobe em `dev` e o Flyway aplica V4 sem erro
- [ ] Scripts espelhados no repo db

## Como testar
Subir no profile `dev` (Flyway aplica) ou rodar o teste de contexto; conferir tipos/constraints.
