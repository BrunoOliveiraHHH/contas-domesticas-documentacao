# Tarefa — Rede: Mercado (Retrofit + repositório) · App
> Sprint 1 (06/07–20/07/2026) · Bloco: Cadastros · Item: Mercado · Passo 2/4 · Depende: Passo 1 (Room)

## O que fazer
Consumir a API de Mercado e criar o repositório (Room + API).

## Passo a passo
1. `data/remote/MercadoApi.kt` (endpoints `/api/v1/mercados`).
2. `data/remote/dto/MercadoDto.kt`.
3. `data/repository/MercadoRepository.kt` (fonte local + remota; sincronização).

## Onde mexer
- `data/remote/MercadoApi.kt`, `data/remote/dto/MercadoDto.kt`, `data/repository/MercadoRepository.kt`

## Critério de pronto (DoD)
- [ ] Repositório compila e expõe os dados (Flow)

## Como testar
Verificação estática + build no Android Studio.
