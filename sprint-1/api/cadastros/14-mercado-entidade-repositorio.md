# Tarefa — Entidade + Repositório: Mercado · API
> Sprint 1 (06/07–20/07/2026) · Bloco: Cadastros · Item: Mercado · Passo 2/6 · Depende: Passo 1 (migração)

## O que fazer
Criar a entidade JPA `Mercado` (estende `BaseEntity`) e o repositório Spring Data.

## Passo a passo
1. Criar `domain/Mercado.java` com `@Entity @Table(name="mercado")` estendendo `BaseEntity`.
2. Mapear os campos: nome, tipo (SUPERMERCADO/CONSTRUCAO/FARMACIA/OUTRO), endereco, bairro, ativo.
3. Criar `repository/MercadoRepository.java` (`JpaRepository<Mercado, Long>`) com as queries necessárias.

## Onde mexer
- `br.com.contasdomesticas.api.domain.Mercado`
- `br.com.contasdomesticas.api.repository.MercadoRepository`

## Critério de pronto (DoD)
- [ ] Hibernate `validate` passa (entidade casa com a tabela)
- [ ] Repositório compila e injeta

## Como testar
`MercadoRepositoryTest` (`@DataJpaTest`): salvar e buscar; conferir auditáveis preenchidos.
