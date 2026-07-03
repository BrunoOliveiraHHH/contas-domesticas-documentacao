# TASK — Usuário e Auditoria · Banco (db)

> Sprint 1 · Contas Domésticas · Projeto DB · Usuário + Auditoria
> (colar no ClickUp) · Modelo-base para as próximas tarefas de DB

## Premissa

- O repositório `db` mantém os **scripts SQL separados** que **espelham** as migrações Flyway da API
  (a fonte de verdade do schema).
- Serve de referência organizada por pasta (`tables`, `primary`, `foreign`, `index`, `inserts`).

## Objetivo

Materializar, em scripts separados, o schema de **usuário** e **auditoria** e o seed do usuário
administrador, alinhados ao Flyway `V1`/`V2`/`V3` da API.

## Especificação

- **`ddl/tables/usuario.sql`** — `create table usuario` (`bigint identity`, login, nome_exibicao,
  senha, campos de auditoria `timestamptz`).
- **`ddl/tables/auditoria.sql`** — `create table auditoria` (usuario, metodo_http, endpoint,
  status_resposta, endereco_ip, data_hora).
- **`ddl/primary/usuario.sql`**, **`ddl/primary/auditoria.sql`** — `pk_usuario`, `pk_auditoria`.
- **`ddl/index/usuario.sql`** — `uk_usuario_login` (único). **`ddl/index/auditoria.sql`** —
  `ix_auditoria_data_hora`, `ix_auditoria_usuario`.
- **`dml/inserts/usuario_admin.sql`** — seed `admin/Admin` (hash BCrypt de "admin"), idempotente
  (`on conflict (login) do nothing`) — espelho do Flyway `V3`.
- `ddl/foreign/` permanece vazio (sem FK; auditoria guarda o login como string, sync-friendly).

## Critérios de Aceite

1. Os scripts refletem **exatamente** o schema criado pelo Flyway da API (tipos, nomes, restrições).
2. Nomes de PK/UK/índices consistentes (`pk_`, `uk_`, `ix_`).
3. O seed admin é **idempotente** e usa o mesmo hash BCrypt do Flyway `V3`.
4. Divisão por pasta respeitada (`tables`/`primary`/`index`/`inserts`).

## Fora de escopo (próximas tarefas de DB)

Ver `PLANO-db.md` (raiz do workspace): Carteira, Cadastros base, Parâmetro/Configuração, Lançamento,
Rateio, Compras, Investimento, colunas de sincronização.
