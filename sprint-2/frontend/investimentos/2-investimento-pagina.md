# Tarefa — Página (lista + formulário): Investimento · Frontend
> Sprint 2 (21/07–04/08/2026) · Bloco: Investimentos · Item: Investimento · Passo 2/3 · Depende: Passo 1 (store)

## O que fazer
Construir a página de Investimento: lista + formulário + aportes.

## Passo a passo
1. `src/pages/InvestimentoPage.vue` (`<script setup>`): `QTable` com os itens do store.
2. Formulário em `QDialog`/`QForm` (campos: nome, tipo, instituição, indexador, taxa, datas; aportes/resgates) com validação e `Notify` de sucesso/erro.
3. Ações criar/editar/remover chamando o store.

## Onde mexer
- `src/pages/InvestimentoPage.vue` (+ componentes em `src/components/`)

## Critério de pronto (DoD)
- [ ] Listar/criar/editar/remover pela tela
- [ ] Validação de formulário funcionando

## Como testar
Vue Test Utils (componente) + `quasar dev` (manual).
