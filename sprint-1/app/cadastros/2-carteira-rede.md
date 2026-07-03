# Tarefa — Rede: Carteira (Retrofit + repositório) · App
> Sprint 1 (06/07–20/07/2026) · Bloco: Cadastros · Item: Carteira · Passo 2/4 · Depende: Passo 1 (Room)

## O que fazer
Consumir a API de Carteira e criar o repositório (Room + API).

## Passo a passo
1. `data/remote/CarteiraApi.kt` (endpoints `/api/v1/carteiras`).
2. `data/remote/dto/CarteiraDto.kt`.
3. `data/repository/CarteiraRepository.kt` (fonte local + remota; sincronização).

## Onde mexer
- `data/remote/CarteiraApi.kt`, `data/remote/dto/CarteiraDto.kt`, `data/repository/CarteiraRepository.kt`

## Critério de pronto (DoD)
- [ ] Repositório compila e expõe os dados (Flow)

## Como testar
Verificação estática + build no Android Studio.
