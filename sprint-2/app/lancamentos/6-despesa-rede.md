# Tarefa — Rede: Despesa (Retrofit + repositório) · App
> Sprint 2 (21/07–04/08/2026) · Bloco: Lançamentos · Item: Despesa · Passo 2/4 · Depende: Passo 1 (Room)

## O que fazer
Consumir a API de Despesa e criar o repositório (Room + API).

## Passo a passo
1. `data/remote/DespesaApi.kt` (endpoints `/api/v1/despesas`).
2. `data/remote/dto/DespesaDto.kt`.
3. `data/repository/DespesaRepository.kt` (fonte local + remota; sincronização).

## Onde mexer
- `data/remote/DespesaApi.kt`, `data/remote/dto/DespesaDto.kt`, `data/repository/DespesaRepository.kt`

## Critério de pronto (DoD)
- [ ] Repositório compila e expõe os dados (Flow)

## Como testar
Verificação estática + build no Android Studio.
