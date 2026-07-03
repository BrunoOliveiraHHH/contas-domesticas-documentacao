# Tarefa — Página (lista + formulário): Unidade de Medida · Frontend
> Sprint 1 (06/07–20/07/2026) · Bloco: Cadastros · Item: Unidade de Medida · Passo 2/3 · Depende: Passo 1 (store)

## O que fazer
Construir a página de Unidade de Medida: lista + formulário; seletor de unidade.

## Passo a passo
1. `src/pages/UnidadedeMedidaPage.vue` (`<script setup>`): `QTable` com os itens do store.
2. Formulário em `QDialog`/`QForm` (campos: nome, sigla, tipo, fator para base) com validação e `Notify` de sucesso/erro.
3. Ações criar/editar/remover chamando o store.

## Onde mexer
- `src/pages/UnidadedeMedidaPage.vue` (+ componentes em `src/components/`)

## Critério de pronto (DoD)
- [ ] Listar/criar/editar/remover pela tela
- [ ] Validação de formulário funcionando

## Como testar
Vue Test Utils (componente) + `quasar dev` (manual).
