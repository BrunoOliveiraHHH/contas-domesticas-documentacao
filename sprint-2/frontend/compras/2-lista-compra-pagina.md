# Tarefa — Página (lista + formulário): Lista de Compra · Frontend
> Sprint 2 (21/07–04/08/2026) · Bloco: Compras · Item: Lista de Compra · Passo 2/3 · Depende: Passo 1 (store)

## O que fazer
Construir a página de Lista de Compra: histórico de listas + formulário; subtotais por estabelecimento; duplicar.

## Passo a passo
1. `src/pages/ListadeCompraPage.vue` (`<script setup>`): `QTable` com os itens do store.
2. Formulário em `QDialog`/`QForm` (campos: nome, tipo, carteira, data, status) com validação e `Notify` de sucesso/erro.
3. Ações criar/editar/remover chamando o store.

## Onde mexer
- `src/pages/ListadeCompraPage.vue` (+ componentes em `src/components/`)

## Critério de pronto (DoD)
- [ ] Listar/criar/editar/remover pela tela
- [ ] Validação de formulário funcionando

## Como testar
Vue Test Utils (componente) + `quasar dev` (manual).
