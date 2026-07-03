# Tarefa — Entidade + Repositório: UnidadeMedida · API
> Sprint 1 (06/07–20/07/2026) · Bloco: Cadastros · Item: UnidadeMedida · Passo 2/6 · Depende: Passo 1 (migração)

## O que fazer
Criar a entidade JPA `UnidadeMedida` (estende `BaseEntity`) e o repositório Spring Data.

## Passo a passo
1. Criar `domain/UnidadeMedida.java` com `@Entity @Table(name="unidade_medida")` estendendo `BaseEntity`.
2. Mapear os campos: nome, sigla (única), tipo (UNIDADE/PESO/VOLUME/COMPRIMENTO), fator_para_base numeric(12,6).
3. Criar `repository/UnidadeMedidaRepository.java` (`JpaRepository<UnidadeMedida, Long>`) com as queries necessárias.

## Onde mexer
- `br.com.contasdomesticas.api.domain.UnidadeMedida`
- `br.com.contasdomesticas.api.repository.UnidadeMedidaRepository`

## Critério de pronto (DoD)
- [ ] Hibernate `validate` passa (entidade casa com a tabela)
- [ ] Repositório compila e injeta

## Como testar
`UnidadeMedidaRepositoryTest` (`@DataJpaTest`): salvar e buscar; conferir auditáveis preenchidos.
