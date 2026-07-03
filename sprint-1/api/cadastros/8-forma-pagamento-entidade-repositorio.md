# Tarefa — Entidade + Repositório: FormaPagamento · API
> Sprint 1 (06/07–20/07/2026) · Bloco: Cadastros · Item: FormaPagamento · Passo 2/6 · Depende: Passo 1 (migração)

## O que fazer
Criar a entidade JPA `FormaPagamento` (estende `BaseEntity`) e o repositório Spring Data.

## Passo a passo
1. Criar `domain/FormaPagamento.java` com `@Entity @Table(name="forma_pagamento")` estendendo `BaseEntity`.
2. Mapear os campos: nome, tipo (DINHEIRO/PIX/DEBITO/CREDITO/BOLETO/TRANSFERENCIA), carteira_id opcional, dia_fechamento/dia_vencimento só crédito, ativa.
3. Criar `repository/FormaPagamentoRepository.java` (`JpaRepository<FormaPagamento, Long>`) com as queries necessárias.

## Onde mexer
- `br.com.contasdomesticas.api.domain.FormaPagamento`
- `br.com.contasdomesticas.api.repository.FormaPagamentoRepository`

## Critério de pronto (DoD)
- [ ] Hibernate `validate` passa (entidade casa com a tabela)
- [ ] Repositório compila e injeta

## Como testar
`FormaPagamentoRepositoryTest` (`@DataJpaTest`): salvar e buscar; conferir auditáveis preenchidos.
