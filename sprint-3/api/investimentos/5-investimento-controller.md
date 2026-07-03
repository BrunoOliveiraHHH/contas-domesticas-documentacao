# Tarefa — Controller (endpoints): Investimento · API
> Sprint 3 (05/08–19/08/2026) · Bloco: Investimentos · Item: Investimento · Passo 5/6 · Depende: Passo 4 (service)

## O que fazer
Expor o CRUD em `/api/v1/investimentos`.

## Passo a passo
1. `controller/InvestimentoController.java` (`@RestController`, `@RequestMapping("/api/v1/investimentos")`).
2. `GET` lista, `GET /{id}`, `POST` (201), `PUT /{id}`, `DELETE /{id}` (204).
3. Delegar ao service e mapear com o mapper.

## Onde mexer
- `br.com.contasdomesticas.api.controller.InvestimentoController`

## Critério de pronto (DoD)
- [ ] Endpoints respondem os códigos corretos (200/201/204/404/409)
- [ ] Rotas exigem autenticação (após o bloco de segurança)

## Como testar
`InvestimentoControllerIntegrationTest` (`@SpringBootTest`+`MockMvc`): CRUD + 404 + payload inválido.
