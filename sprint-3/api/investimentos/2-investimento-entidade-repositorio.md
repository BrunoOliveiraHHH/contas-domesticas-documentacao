# Tarefa — Entidade + Repositório: Investimento · API
> Sprint 3 (05/08–19/08/2026) · Bloco: Investimentos · Item: Investimento · Passo 2/6 · Depende: Passo 1 (migração)

## O que fazer
Criar a entidade JPA `Investimento` (estende `BaseEntity`) e o repositório Spring Data.

## Passo a passo
1. Criar `domain/Investimento.java` com `@Entity @Table(name="investimento")` estendendo `BaseEntity`.
2. Mapear os campos: nome, tipo_investimento (RENDA_FIXA/RENDA_VARIAVEL/FUNDO/CRIPTO/PREVIDENCIA/POUPANCA/RESERVA_EMERGENCIA), instituicao, carteira_id, indexador (SELIC/CDI/IPCA/PRE), taxa_contratada, data_aplicacao, data_vencimento.
3. Criar `repository/InvestimentoRepository.java` (`JpaRepository<Investimento, Long>`) com as queries necessárias.

## Onde mexer
- `br.com.contasdomesticas.api.domain.Investimento`
- `br.com.contasdomesticas.api.repository.InvestimentoRepository`

## Critério de pronto (DoD)
- [ ] Hibernate `validate` passa (entidade casa com a tabela)
- [ ] Repositório compila e injeta

## Como testar
`InvestimentoRepositoryTest` (`@DataJpaTest`): salvar e buscar; conferir auditáveis preenchidos.
