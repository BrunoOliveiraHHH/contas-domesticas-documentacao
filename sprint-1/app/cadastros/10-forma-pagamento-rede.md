# Tarefa — Rede: Forma de Pagamento (Retrofit + repositório) · App
> Sprint 1 (06/07–20/07/2026) · Bloco: Cadastros · Item: Forma de Pagamento · Passo 2/4 · Depende: Passo 1 (Room)

## O que fazer
Consumir a API de Forma de Pagamento e criar o repositório (Room + API).

## Passo a passo
1. `data/remote/FormaPagamentoApi.kt` (endpoints `/api/v1/formas-pagamento`).
2. `data/remote/dto/FormaPagamentoDto.kt`.
3. `data/repository/FormaPagamentoRepository.kt` (fonte local + remota; sincronização).

## Onde mexer
- `data/remote/FormaPagamentoApi.kt`, `data/remote/dto/FormaPagamentoDto.kt`, `data/repository/FormaPagamentoRepository.kt`

## Critério de pronto (DoD)
- [ ] Repositório compila e expõe os dados (Flow)

## Como testar
Verificação estática + build no Android Studio.
