# Tarefa — Boot Axios + client da API · Frontend
> Sprint 1 (06/07–20/07/2026) · Bloco: Fundação Quasar · Passo 3/4 · Depende: projeto

## O que fazer
Configurar a instância Axios que fala com a API.

## Passo a passo
1. `src/boot/axios.js`: instância com `baseURL` = `API_URL`; expor via `provide`/`app.config.globalProperties`.
2. Tratamento de erro global (interceptor de resposta → `Notify`).

## Onde mexer
- `src/boot/axios.js`, `quasar.config.js` (boot: ['axios'])

## Critério de pronto (DoD)
- [ ] Chamadas usam a `baseURL` correta; erros mostram Notify

## Como testar
`quasar dev` (chamada de teste a `/actuator/health` ou similar).
