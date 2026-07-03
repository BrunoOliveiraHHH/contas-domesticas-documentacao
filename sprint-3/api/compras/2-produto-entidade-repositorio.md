# Tarefa — Entidade + Repositório: Produto · API
> Sprint 3 (05/08–19/08/2026) · Bloco: Compras · Item: Produto · Passo 2/6 · Depende: Passo 1 (migração)

## O que fazer
Criar a entidade JPA `Produto` (estende `BaseEntity`) e o repositório Spring Data.

## Passo a passo
1. Criar `domain/Produto.java` com `@Entity @Table(name="produto")` estendendo `BaseEntity`.
2. Mapear os campos: nome, descricao, categoria_id, unidade_medida_padrao_id, codigo_barras (opcional), ativo boolean.
3. Criar `repository/ProdutoRepository.java` (`JpaRepository<Produto, Long>`) com as queries necessárias.

## Onde mexer
- `br.com.contasdomesticas.api.domain.Produto`
- `br.com.contasdomesticas.api.repository.ProdutoRepository`

## Critério de pronto (DoD)
- [ ] Hibernate `validate` passa (entidade casa com a tabela)
- [ ] Repositório compila e injeta

## Como testar
`ProdutoRepositoryTest` (`@DataJpaTest`): salvar e buscar; conferir auditáveis preenchidos.
