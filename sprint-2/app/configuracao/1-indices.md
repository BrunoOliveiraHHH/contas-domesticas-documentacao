# Tarefa — Configuração: índices financeiros · App
> Sprint 2 (21/07–04/08/2026) · Bloco: Configuração · Passo 1/4 · Depende: API parâmetros

## O que fazer
Ver/editar Selic/CDI/IPCA na tela de Configuração.

## Passo a passo
1. `ParametroEntity` + DAO + repositório (sincroniza com a API).
2. Seção "Índices" (valor + vigência).

## Onde mexer
- `ui/config/*`, `data/local/entity/ParametroEntity.kt`

## Critério de pronto (DoD)
- [ ] Editar/consultar índices; sincroniza com a API

## Como testar
Verificação estática + build no Android Studio.
