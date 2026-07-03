# Tarefa — Página (lista + formulário): Categoria · Frontend
> Sprint 1 (06/07–20/07/2026) · Bloco: Cadastros · Item: Categoria · Passo 2/3 · Depende: Passo 1 (store)

## O que fazer
Construir a página de Categoria: árvore + formulário; seletor por tipo.

## Passo a passo
1. `src/pages/CategoriaPage.vue` (`<script setup>`): `QTable` com os itens do store.
2. Formulário em `QDialog`/`QForm` (campos: nome, tipo, categoria pai, cor, ícone, ativa) com validação e `Notify` de sucesso/erro.
3. Ações criar/editar/remover chamando o store.

## Onde mexer
- `src/pages/CategoriaPage.vue` (+ componentes em `src/components/`)

## Critério de pronto (DoD)
- [ ] Listar/criar/editar/remover pela tela
- [ ] Validação de formulário funcionando

## Como testar
Vue Test Utils (componente) + `quasar dev` (manual).
