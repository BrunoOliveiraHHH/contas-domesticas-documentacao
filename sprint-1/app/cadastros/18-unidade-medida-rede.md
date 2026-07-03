# Tarefa — Rede: Unidade de Medida (Retrofit + repositório) · App
> Sprint 1 (06/07–20/07/2026) · Bloco: Cadastros · Item: Unidade de Medida · Passo 2/4 · Depende: Passo 1 (Room)

## O que fazer
Consumir a API de Unidade de Medida e criar o repositório (Room + API).

## Passo a passo
1. `data/remote/UnidadeMedidaApi.kt` (endpoints `/api/v1/unidades-medida`).
2. `data/remote/dto/UnidadeMedidaDto.kt`.
3. `data/repository/UnidadeMedidaRepository.kt` (fonte local + remota; sincronização).

## Onde mexer
- `data/remote/UnidadeMedidaApi.kt`, `data/remote/dto/UnidadeMedidaDto.kt`, `data/repository/UnidadeMedidaRepository.kt`

## Critério de pronto (DoD)
- [ ] Repositório compila e expõe os dados (Flow)

## Como testar
Verificação estática + build no Android Studio.
