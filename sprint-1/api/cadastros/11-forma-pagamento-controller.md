# Tarefa — Controller (endpoints): FormaPagamento · API
> Sprint 1 (06/07–20/07/2026) · Bloco: Cadastros · Item: FormaPagamento · Passo 5/6 · Depende: Passo 4 (service)

## O que fazer
Expor o CRUD em `/api/v1/formas-pagamento`.

## Passo a passo
1. `controller/FormaPagamentoController.java` (`@RestController`, `@RequestMapping("/api/v1/formas-pagamento")`).
2. `GET` lista, `GET /{id}`, `POST` (201), `PUT /{id}`, `DELETE /{id}` (204).
3. Delegar ao service e mapear com o mapper.

## Onde mexer
- `br.com.contasdomesticas.api.controller.FormaPagamentoController`

## Critério de pronto (DoD)
- [ ] Endpoints respondem os códigos corretos (200/201/204/404/409)
- [ ] Rotas exigem autenticação (após o bloco de segurança)

## Como testar
`FormaPagamentoControllerIntegrationTest` (`@SpringBootTest`+`MockMvc`): CRUD + 404 + payload inválido.
