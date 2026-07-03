# Tarefa — Página (lista + formulário): Forma de Pagamento · Frontend
> Sprint 1 (06/07–20/07/2026) · Bloco: Cadastros · Item: Forma de Pagamento · Passo 2/3 · Depende: Passo 1 (store)

## O que fazer
Construir a página de Forma de Pagamento: lista + formulário (campos de crédito condicionais).

## Passo a passo
1. `src/pages/FormadePagamentoPage.vue` (`<script setup>`): `QTable` com os itens do store.
2. Formulário em `QDialog`/`QForm` (campos: nome, tipo, carteira, dias de crédito, ativa) com validação e `Notify` de sucesso/erro.
3. Ações criar/editar/remover chamando o store.

## Onde mexer
- `src/pages/FormadePagamentoPage.vue` (+ componentes em `src/components/`)

## Critério de pronto (DoD)
- [ ] Listar/criar/editar/remover pela tela
- [ ] Validação de formulário funcionando

## Como testar
Vue Test Utils (componente) + `quasar dev` (manual).
