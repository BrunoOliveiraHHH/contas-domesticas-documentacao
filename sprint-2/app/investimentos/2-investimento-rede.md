# Tarefa — Rede: Investimento (Retrofit + repositório) · App
> Sprint 2 (21/07–04/08/2026) · Bloco: Investimentos · Item: Investimento · Passo 2/4 · Depende: Passo 1 (Room)

## O que fazer
Consumir a API de Investimento e criar o repositório (Room + API).

## Passo a passo
1. `data/remote/InvestimentoApi.kt` (endpoints `/api/v1/investimentos`).
2. `data/remote/dto/InvestimentoDto.kt`.
3. `data/repository/InvestimentoRepository.kt` (fonte local + remota; sincronização).

## Onde mexer
- `data/remote/InvestimentoApi.kt`, `data/remote/dto/InvestimentoDto.kt`, `data/repository/InvestimentoRepository.kt`

## Critério de pronto (DoD)
- [ ] Repositório compila e expõe os dados (Flow)

## Como testar
Verificação estática + build no Android Studio.
