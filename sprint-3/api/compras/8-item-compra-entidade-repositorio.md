# Tarefa — Entidade + Repositório: ItemCompra · API
> Sprint 3 (05/08–19/08/2026) · Bloco: Compras · Item: ItemCompra · Passo 2/6 · Depende: Passo 1 (migração)

## O que fazer
Criar a entidade JPA `ItemCompra` (estende `BaseEntity`) e o repositório Spring Data.

## Passo a passo
1. Criar `domain/ItemCompra.java` com `@Entity @Table(name="item_compra")` estendendo `BaseEntity`.
2. Mapear os campos: lista_compra_id (FK), produto, categoria_id opcional, quantidade numeric(12,3), unidade_medida_id, preco_unitario_estimado, preco_unitario_real, comprado boolean, mercado_id override.
3. Criar `repository/ItemCompraRepository.java` (`JpaRepository<ItemCompra, Long>`) com as queries necessárias.

## Onde mexer
- `br.com.contasdomesticas.api.domain.ItemCompra`
- `br.com.contasdomesticas.api.repository.ItemCompraRepository`

## Critério de pronto (DoD)
- [ ] Hibernate `validate` passa (entidade casa com a tabela)
- [ ] Repositório compila e injeta

## Como testar
`ItemCompraRepositoryTest` (`@DataJpaTest`): salvar e buscar; conferir auditáveis preenchidos.
