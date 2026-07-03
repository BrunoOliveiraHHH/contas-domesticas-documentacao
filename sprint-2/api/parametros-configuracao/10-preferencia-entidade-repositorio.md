# Tarefa — Entidade + Repositório: Preferencia · API
> Sprint 2 (21/07–04/08/2026) · Bloco: Parâmetros & Configuração · Item: Preferencia · Passo 2/6 · Depende: Passo 1 (migração)

## O que fazer
Criar a entidade JPA `Preferencia` (estende `BaseEntity`) e o repositório Spring Data.

## Passo a passo
1. Criar `domain/Preferencia.java` com `@Entity @Table(name="preferencia")` estendendo `BaseEntity`.
2. Mapear os campos: chave (CARTEIRA_PADRAO/REGRA_RATEIO/INICIO_MES/MOEDA/...), valor, usuario_id (nulo=global).
3. Criar `repository/PreferenciaRepository.java` (`JpaRepository<Preferencia, Long>`) com as queries necessárias.

## Onde mexer
- `br.com.contasdomesticas.api.domain.Preferencia`
- `br.com.contasdomesticas.api.repository.PreferenciaRepository`

## Critério de pronto (DoD)
- [ ] Hibernate `validate` passa (entidade casa com a tabela)
- [ ] Repositório compila e injeta

## Como testar
`PreferenciaRepositoryTest` (`@DataJpaTest`): salvar e buscar; conferir auditáveis preenchidos.
