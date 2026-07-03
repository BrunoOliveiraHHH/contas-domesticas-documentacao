# Tarefa — Entidade + Repositório: Carteira · API
> Sprint 1 (06/07–20/07/2026) · Bloco: Carteiras · Item: Carteira · Passo 2/6 · Depende: Passo 1 (migração)

## O que fazer
Criar a entidade JPA `Carteira` (estende `BaseEntity`) e o repositório Spring Data.

## Passo a passo
1. Criar `domain/Carteira.java` com `@Entity @Table(name="carteira")` estendendo `BaseEntity`.
2. Mapear os campos: nome, tipo (FAMILIAR/INDIVIDUAL), dono_id (nulo se familiar), saldo_inicial numeric(15,2), moeda varchar(3) default 'BRL', cor, icone, ativa boolean.
3. Criar `repository/CarteiraRepository.java` (`JpaRepository<Carteira, Long>`) com as queries necessárias.

## Onde mexer
- `br.com.contasdomesticas.api.domain.Carteira`
- `br.com.contasdomesticas.api.repository.CarteiraRepository`

## Critério de pronto (DoD)
- [ ] Hibernate `validate` passa (entidade casa com a tabela)
- [ ] Repositório compila e injeta

## Como testar
`CarteiraRepositoryTest` (`@DataJpaTest`): salvar e buscar; conferir auditáveis preenchidos.
