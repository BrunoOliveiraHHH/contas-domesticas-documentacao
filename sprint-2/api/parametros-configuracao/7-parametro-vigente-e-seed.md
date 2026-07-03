# Tarefa — Endpoint vigente + seed de índices · API
> Sprint 2 (21/07–04/08/2026) · Bloco: Parâmetros & Configuração · Complemento Parametro · Depende: Parametro (CRUD)

## O que fazer
Expor a consulta do valor vigente e semear os índices iniciais.

## Passo a passo
1. `GET /api/v1/parametros/{chave}/vigente` retorna o valor com maior `vigencia_inicio` menor/igual a hoje.
2. Seed inicial (Selic/CDI/IPCA) via Flyway ou `data.sql` de dev.

## Onde mexer
- `ParametroController` / `ParametroService`

## Critério de pronto (DoD)
- [ ] Vigente por data retorna o valor correto
- [ ] Índices semeados em dev

## Como testar
`ParametroServiceTest.deveResolverVigentePorData`.
