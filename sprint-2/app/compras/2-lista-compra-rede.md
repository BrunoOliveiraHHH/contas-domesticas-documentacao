# Tarefa — Rede: Lista de Compra (Retrofit + repositório) · App
> Sprint 2 (21/07–04/08/2026) · Bloco: Compras · Item: Lista de Compra · Passo 2/4 · Depende: Passo 1 (Room)

## O que fazer
Consumir a API de Lista de Compra e criar o repositório (Room + API).

## Passo a passo
1. `data/remote/ListaCompraApi.kt` (endpoints `/api/v1/listas-compra`).
2. `data/remote/dto/ListaCompraDto.kt`.
3. `data/repository/ListaCompraRepository.kt` (fonte local + remota; sincronização).

## Onde mexer
- `data/remote/ListaCompraApi.kt`, `data/remote/dto/ListaCompraDto.kt`, `data/repository/ListaCompraRepository.kt`

## Critério de pronto (DoD)
- [ ] Repositório compila e expõe os dados (Flow)

## Como testar
Verificação estática + build no Android Studio.
