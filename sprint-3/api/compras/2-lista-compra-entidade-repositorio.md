# Tarefa — Entidade + Repositório: ListaCompra · API
> Sprint 3 (05/08–19/08/2026) · Bloco: Compras · Item: ListaCompra · Passo 2/6 · Depende: Passo 1 (migração)

## O que fazer
Criar a entidade JPA `ListaCompra` (estende `BaseEntity`) e o repositório Spring Data.

## Passo a passo
1. Criar `domain/ListaCompra.java` com `@Entity @Table(name="lista_compra")` estendendo `BaseEntity`.
2. Mapear os campos: nome, tipo (MANTIMENTOS/CONSTRUCAO), carteira_id, data, status (ABERTA/FECHADA/ARQUIVADA).
3. Criar `repository/ListaCompraRepository.java` (`JpaRepository<ListaCompra, Long>`) com as queries necessárias.

## Onde mexer
- `br.com.contasdomesticas.api.domain.ListaCompra`
- `br.com.contasdomesticas.api.repository.ListaCompraRepository`

## Critério de pronto (DoD)
- [ ] Hibernate `validate` passa (entidade casa com a tabela)
- [ ] Repositório compila e injeta

## Como testar
`ListaCompraRepositoryTest` (`@DataJpaTest`): salvar e buscar; conferir auditáveis preenchidos.
