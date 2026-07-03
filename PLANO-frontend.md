# Plano de Desenvolvimento — Frontend Web (`contas-domesticas-front`)

> Contas Domésticas · SPA **Vue 3 + Quasar (app-vite v2) + TypeScript** · Pinia · Vue Router · Axios
> **Node 24** (`.nvmrc`, via NVS). Roadmap **completo e detalhado**, item a item (sem agrupar). A
> **ordem** segue a dependência técnica; cada item traz componentes, integração, regras e aceite.

## Visão

Interface **web** do Contas Domésticas, consumindo a **API local** (mesma dos apps). Cobre **finanças
familiar e individual** (via carteiras), **compras** (catálogo de produtos, cotação por estabelecimento,
comparar/escolher, fechar por loja, reutilizar listas), **investimentos**, **calculadoras**,
**Configuração** parametrizável e **Dashboard**. Diferente do app Android (offline-first), o front é
**online** — fala direto com a API, sem banco local nem sincronização.

### Convenções aplicadas a todos os itens
- **Stack:** Vue 3 (`<script setup lang="ts">`, Composition API), **Quasar v2** (**app-vite v2**,
  wrappers `#q-app/wrappers`), **TypeScript**, **Pinia** (estado, com `pinia-plugin-persistedstate`),
  **Vue Router**, **Axios** (boot com `baseURL` da API + `axios-retry` + interceptors). **Node 24**.
- **Estrutura:** `src/` → `boot/` (axios, vue-query, i18n, echarts), `layouts/` (MainLayout), `pages/`,
  `components/`, `stores/` (Pinia), `router/` (routes.ts), `services/` (chamadas à API),
  `composables/`, `i18n/`, `util/` (money/date), `css/`. PWA em `src-pwa/`.
- **Padrão por feature (CRUD):** `services/<x>.ts` (Axios) → `stores/<x>.ts` (Pinia) → `pages`
  (lista `QTable` + formulário `QDialog`/`QForm`) → rota + item no menu. Estado de servidor via
  **@tanstack/vue-query**; validação com **vee-validate + zod**; utilitários com **@vueuse/core**.
- **UI:** componentes Quasar (`QTable`, `QForm`, `QInput`, `QSelect`, `QDialog`, `QBtn`, `Notify`,
  `Dialog`); gráficos com **ECharts** (`<v-chart>`, boot global); i18n **vue-i18n** (pt-BR);
  moeda com **big.js** (decimal) e datas com **date-fns**.
- **Auth:** JWT no store persistido; interceptor injeta `Bearer` e renova no 401; **route guards**.
- **Testes/DX:** **Vitest** (+ `@vue/test-utils`, `@pinia/testing`, jsdom), **Cypress** (e2e),
  **ESLint + Prettier**, **husky + lint-staged** (pre-commit), `vue-tsc` (`npm run typecheck`).
- **Escopo (familiar/individual):** derivado da **carteira** selecionada (mesma regra da API).

## Roadmap por bloco (4 blocos/sprint · 15 dias · início 06/07/2026)

### Sprint 1 (06/07–20/07)

**Bloco `fundacao-quasar`** — base do projeto
| Item | O que é | Depende |
|------|---------|---------|
| Projeto + estrutura | Quasar CLI (Vite), pastas, env (`API_URL`) | — |
| Layout + tema | `MainLayout` (QLayout/QHeader/QDrawer), menu, variáveis de tema | projeto |
| Boot Axios | instância Axios (`baseURL`), tratamento de erro global (Notify) | projeto |
| Router + Pinia | rotas base, guarda placeholder, Pinia instalado | projeto |

**Bloco `autenticacao`** — login/JWT
| Item | O que é | Depende |
|------|---------|---------|
| Store de auth + token | Pinia `auth` (token/usuário) + persistência | fundação |
| Interceptor | injeta `Bearer`; renova no 401 (`/auth/refresh`) | store auth, api-auth |
| Página de login | `LoginPage` (QForm) → `/auth/login` → guarda token | interceptor |
| Guards + logout | rotas protegidas; logout limpa token | login |

**Bloco `cadastros`** — CRUDs (padrão por feature): **Produto (catálogo)**, **Carteira**,
**Categoria**, **Forma de Pagamento**, **Mercado**, **Unidade de Medida** (cada um: service+store →
página lista/form → rota+menu). Depende: autenticação + endpoints de cadastro da API.

**Bloco `configuracao`** — Índices (Selic/CDI/IPCA), Alíquotas (IR/IOF), Preferências (carteira
padrão, regra de rateio, início do mês, moeda), Segurança (troca de senha). Depende: cadastros +
api-parâmetros.

### Sprint 2 (21/07–04/08)

**Bloco `lancamentos`** — **Receita** e **Despesa** (CRUD + status/vencimento), **Recorrência**,
**Parcelamento**, **Rateio + acerto**. Depende: cadastros + api-lançamentos.

**Bloco `compras`** — **Lista** (histórico + duplicar), **Item** (do catálogo) **+ escolha de
estabelecimento**, **Cotação de produto** (comparar por preço/unidade), **Fechar → despesa por
estabelecimento**. Depende: cadastro de Produto/Mercado + api-compras.

**Bloco `investimentos`** — **Cadastro + aportes**, **Evolução** (gráfico). Depende: carteira +
api-investimentos.

**Bloco `calculadoras`** — **Investimento**, **IR sobre investimentos**, **Financiamento (Price/SAC)**,
**Preço por unidade**. Cálculo client-side (composables) + página; usa parâmetros da Configuração.

### Sprint 3 (05/08–19/08)

**Bloco `dashboard`** — **Resumo do mês**, **Gastos por categoria** (gráfico), **Evolução
patrimonial** (gráfico). Depende: lançamentos/investimentos + api-relatórios.

**Bloco `testes`** — **Unitários (Vitest)**, **Componentes (Vue Test Utils)**, **E2E (Cypress)** dos
fluxos-chave (login, criar despesa, fechar lista → despesa).

## Verificação
- Node 24 (`nvs use 24`), `npm install`, `npm run typecheck` (`vue-tsc`).
- `quasar dev` apontando para a API local; `quasar build` (produção); `build:pwa` para o modo PWA.
- `vitest` (unit/componentes) e `cypress` (e2e) verdes no CI (GitHub Actions em Node 24).

## Fora de escopo
Sincronização/offline-first (o front é **online**; o PWA dá cache/instalável, não substitui o sync do
app Android), SSR, i18n multilíngue (só pt-BR por ora), temas white-label.
