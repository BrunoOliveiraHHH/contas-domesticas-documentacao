# Tarefa — Fiação Hilt + navegação: Investimento · App
> Sprint 2 (21/07–04/08/2026) · Bloco: Investimentos · Item: Investimento · Passo 4/4 · Depende: Passo 3 (tela)

## O que fazer
Injetar as dependências e ligar a tela à navegação.

## Passo a passo
1. Prover DAO/Api/Repository nos módulos Hilt (`DatabaseModule`/`NetworkModule`).
2. Adicionar a rota no `NavHost` e o acesso na navegação.

## Onde mexer
- `di/DatabaseModule.kt`, `di/NetworkModule.kt`, navegação Compose

## Critério de pronto (DoD)
- [ ] Tela acessível pela navegação com dependências injetadas

## Como testar
Verificação estática + build no Android Studio.
