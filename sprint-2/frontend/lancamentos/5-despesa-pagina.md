# Tarefa — Página (lista + formulário): Despesa · Frontend
> Sprint 2 (21/07–04/08/2026) · Bloco: Lançamentos · Item: Despesa · Passo 2/3 · Depende: Passo 1 (store)

## O que fazer
Construir a página de Despesa: lista + formulário; marcar como pago.

## Passo a passo
1. `src/pages/DespesaPage.vue` (`<script setup>`): `QTable` com os itens do store.
2. Formulário em `QDialog`/`QForm` (campos: valor, vencimento, status, carteira, categoria, forma de pagamento) com validação e `Notify` de sucesso/erro.
3. Ações criar/editar/remover chamando o store.

## Onde mexer
- `src/pages/DespesaPage.vue` (+ componentes em `src/components/`)

## Critério de pronto (DoD)
- [ ] Listar/criar/editar/remover pela tela
- [ ] Validação de formulário funcionando

## Como testar
Vue Test Utils (componente) + `quasar dev` (manual).
