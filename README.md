# contas-domesticas-documentacao

Documentação e planejamento do projeto **Contas Domésticas**.

## Propósito

O **Contas Domésticas** é um app de uso próprio (família) que unifica **finanças familiar e
individual** (receitas, despesas e investimentos por **carteira**, com recorrência, parcelamento e
**rateio**), **listas de compras** (mantimentos e material de construção por unidade/kg/volume, com
histórico de preço; ao fechar, a lista vira despesa), **investimentos**, **calculadoras**
(investimento, IR, financiamento, preço por unidade) e uma **Configuração** parametrizável (índices
Selic/CDI/IPCA e alíquotas IR/IOF).

Ecossistema de repositórios:

| Repositório | Papel |
|-------------|-------|
| `contas-domesticas-api` | Backend Spring Boot (domínio, REST, sincronização) |
| `contas-domesticas-app` | App Android (offline-first, Room + Compose) |
| `contas-domesticas-db` | Scripts SQL (espelho do Flyway da API) |
| `contas-domesticas-documentacao` | **Este repo** — roadmap e tarefas |

Este repositório concentra o **planejamento** (roadmap por projeto) e as **tarefas** por sprint
(modelo ClickUp).

## Estrutura

```
PLANO-api.md      # roadmap completo da API (itens com dependência/ordem)
PLANO-app.md      # roadmap completo do app Android
PLANO-db.md       # roadmap completo do banco (tabela a tabela)
sprint-1/
├── api/          # tarefas da sprint por projeto (1-usuario-e-auditoria.md, ...)
├── app/
└── db/
```

- **`PLANO-*.md`** — visão do todo, item a item, para fatiar em sprints.
- **`sprint-1/<projeto>/`** — tarefas numeradas (1, 2, ...) no modelo Premissa · Objetivo ·
  Especificação · Critérios de Aceite · Cenários de Teste, prontas para colar no ClickUp. A tarefa
  **Usuário + Auditoria** (nº 1) serve de base/modelo para as próximas.

## Status

- **Sprint 1 — Usuário + Auditoria:** implementada na API (suíte automatizada verde) e espelhada no
  app e no banco. Documentada em `sprint-1/{api,app,db}/1-usuario-e-auditoria.md`.
