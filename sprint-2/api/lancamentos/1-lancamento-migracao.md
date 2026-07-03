# Tarefa — Migração Flyway: tabela lancamento · API
> Sprint 2 (21/07–04/08/2026) · Bloco: Lançamentos · Item Lançamento base · Passo 1 · Depende: Carteiras, Cadastros

## O que fazer
Criar a migração `V11` da tabela `lancamento` (núcleo de receita e despesa) e espelhar no db.

## Passo a passo
1. `V11__cria_tabela_lancamento.sql`: id, tipo (RECEITA/DESPESA), descricao, valor numeric(15,2), data_competencia, data_vencimento, data_pagamento, status, carteira_id, categoria_id, forma_pagamento_id, observacao, anexo_url + auditoria.
2. FKs para carteira/categoria/forma_pagamento; índices (competência, carteira, tipo/status).
3. Espelhar no repo db.

## Onde mexer
- `.../db/migration/V11__cria_tabela_lancamento.sql` e `contas-domesticas-db/ddl/*`

## Critério de pronto (DoD)
- [ ] Flyway aplica V11 em dev

## Como testar
Subir em dev; conferir FKs/índices.
