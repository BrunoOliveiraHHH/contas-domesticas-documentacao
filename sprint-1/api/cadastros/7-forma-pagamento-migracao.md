# Tarefa — Migração Flyway: tabela `forma_pagamento` · API
> Sprint 1 (06/07–20/07/2026) · Bloco: Cadastros · Item: FormaPagamento · Passo 1/6 · Depende: base do projeto

## O que fazer
Criar a migração Flyway **V6** que cria a tabela `forma_pagamento` e espelhar os scripts no repo `contas-domesticas-db`.

## Passo a passo
1. Criar `src/main/resources/db/migration/V6__cria_tabela_forma_pagamento.sql`.
2. Colunas: id `bigint generated always as identity` + nome, tipo (DINHEIRO/PIX/DEBITO/CREDITO/BOLETO/TRANSFERENCIA), carteira_id opcional, dia_fechamento/dia_vencimento só crédito, ativa + auditoria (`criado_em`, `criado_por`, `atualizado_em`, `atualizado_por`).
3. Adicionar PK (`pk_forma_pagamento`) e índices/único necessários.
4. Espelhar em `contas-domesticas-db/ddl/{tables,primary,index}/forma_pagamento.sql`.

## Onde mexer
- `contas-domesticas-api/src/main/resources/db/migration/V6__cria_tabela_forma_pagamento.sql`
- `contas-domesticas-db/ddl/{tables,primary,index}/forma_pagamento.sql`

## Critério de pronto (DoD)
- [ ] App sobe em `dev` e o Flyway aplica V6 sem erro
- [ ] Scripts espelhados no repo db

## Como testar
Subir no profile `dev` (Flyway aplica) ou rodar o teste de contexto; conferir tipos/constraints.
