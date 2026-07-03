# Tarefa — Entidade + Repositório: Lancamento · API
> Sprint 2 (21/07–04/08/2026) · Bloco: Lançamentos · Item Lançamento base · Passo 2 · Depende: migração V11

## O que fazer
Criar a entidade `Lancamento` (estende `BaseEntity`) e o repositório com as consultas base.

## Passo a passo
1. `domain/Lancamento.java` (`@Entity`, tipo enum RECEITA/DESPESA, FKs).
2. `repository/LancamentoRepository.java`: por carteira, por competência (mês), por categoria, por tipo.

## Onde mexer
- `.../domain/Lancamento`, `.../repository/LancamentoRepository`

## Critério de pronto (DoD)
- [ ] `validate` passa; consultas compilam

## Como testar
`LancamentoRepositoryTest`: persistir + consultar por competência/tipo.
