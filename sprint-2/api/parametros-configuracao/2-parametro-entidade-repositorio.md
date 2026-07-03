# Tarefa — Entidade + Repositório: Parametro · API
> Sprint 2 (21/07–04/08/2026) · Bloco: Parâmetros & Configuração · Item: Parametro · Passo 2/6 · Depende: Passo 1 (migração)

## O que fazer
Criar a entidade JPA `Parametro` (estende `BaseEntity`) e o repositório Spring Data.

## Passo a passo
1. Criar `domain/Parametro.java` com `@Entity @Table(name="parametro")` estendendo `BaseEntity`.
2. Mapear os campos: chave (SELIC/CDI/IPCA/...), valor numeric(9,4), vigencia_inicio date, descricao.
3. Criar `repository/ParametroRepository.java` (`JpaRepository<Parametro, Long>`) com as queries necessárias.

## Onde mexer
- `br.com.contasdomesticas.api.domain.Parametro`
- `br.com.contasdomesticas.api.repository.ParametroRepository`

## Critério de pronto (DoD)
- [ ] Hibernate `validate` passa (entidade casa com a tabela)
- [ ] Repositório compila e injeta

## Como testar
`ParametroRepositoryTest` (`@DataJpaTest`): salvar e buscar; conferir auditáveis preenchidos.
