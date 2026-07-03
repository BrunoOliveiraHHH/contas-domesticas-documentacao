# Tarefa — Rede: Receita (Retrofit + repositório) · App
> Sprint 2 (21/07–04/08/2026) · Bloco: Lançamentos · Item: Receita · Passo 2/4 · Depende: Passo 1 (Room)

## O que fazer
Consumir a API de Receita e criar o repositório (Room + API).

## Passo a passo
1. `data/remote/ReceitaApi.kt` (endpoints `/api/v1/receitas`).
2. `data/remote/dto/ReceitaDto.kt`.
3. `data/repository/ReceitaRepository.kt` (fonte local + remota; sincronização).

## Onde mexer
- `data/remote/ReceitaApi.kt`, `data/remote/dto/ReceitaDto.kt`, `data/repository/ReceitaRepository.kt`

## Critério de pronto (DoD)
- [ ] Repositório compila e expõe os dados (Flow)

## Como testar
Verificação estática + build no Android Studio.
