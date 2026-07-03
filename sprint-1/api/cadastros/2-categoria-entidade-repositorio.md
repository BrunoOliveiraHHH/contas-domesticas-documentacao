# Tarefa — Entidade + Repositório: Categoria · API
> Sprint 1 (06/07–20/07/2026) · Bloco: Cadastros · Item: Categoria · Passo 2/6 · Depende: Passo 1 (migração)

## O que fazer
Criar a entidade JPA `Categoria` (estende `BaseEntity`) e o repositório Spring Data.

## Passo a passo
1. Criar `domain/Categoria.java` com `@Entity @Table(name="categoria")` estendendo `BaseEntity`.
2. Mapear os campos: nome, tipo (RECEITA/DESPESA/INVESTIMENTO), categoria_pai_id (self, nulo na raiz), cor, icone, ativa.
3. Criar `repository/CategoriaRepository.java` (`JpaRepository<Categoria, Long>`) com as queries necessárias.

## Onde mexer
- `br.com.contasdomesticas.api.domain.Categoria`
- `br.com.contasdomesticas.api.repository.CategoriaRepository`

## Critério de pronto (DoD)
- [ ] Hibernate `validate` passa (entidade casa com a tabela)
- [ ] Repositório compila e injeta

## Como testar
`CategoriaRepositoryTest` (`@DataJpaTest`): salvar e buscar; conferir auditáveis preenchidos.
