# Tarefa — Rede: Categoria (Retrofit + repositório) · App
> Sprint 1 (06/07–20/07/2026) · Bloco: Cadastros · Item: Categoria · Passo 2/4 · Depende: Passo 1 (Room)

## O que fazer
Consumir a API de Categoria e criar o repositório (Room + API).

## Passo a passo
1. `data/remote/CategoriaApi.kt` (endpoints `/api/v1/categorias`).
2. `data/remote/dto/CategoriaDto.kt`.
3. `data/repository/CategoriaRepository.kt` (fonte local + remota; sincronização).

## Onde mexer
- `data/remote/CategoriaApi.kt`, `data/remote/dto/CategoriaDto.kt`, `data/repository/CategoriaRepository.kt`

## Critério de pronto (DoD)
- [ ] Repositório compila e expõe os dados (Flow)

## Como testar
Verificação estática + build no Android Studio.
