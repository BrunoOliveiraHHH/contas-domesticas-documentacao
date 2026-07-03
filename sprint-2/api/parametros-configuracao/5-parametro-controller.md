# Tarefa — Controller (endpoints): Parametro · API
> Sprint 2 (21/07–04/08/2026) · Bloco: Parâmetros & Configuração · Item: Parametro · Passo 5/6 · Depende: Passo 4 (service)

## O que fazer
Expor o CRUD em `/api/v1/parametros`.

## Passo a passo
1. `controller/ParametroController.java` (`@RestController`, `@RequestMapping("/api/v1/parametros")`).
2. `GET` lista, `GET /{id}`, `POST` (201), `PUT /{id}`, `DELETE /{id}` (204).
3. Delegar ao service e mapear com o mapper.

## Onde mexer
- `br.com.contasdomesticas.api.controller.ParametroController`

## Critério de pronto (DoD)
- [ ] Endpoints respondem os códigos corretos (200/201/204/404/409)
- [ ] Rotas exigem autenticação (após o bloco de segurança)

## Como testar
`ParametroControllerIntegrationTest` (`@SpringBootTest`+`MockMvc`): CRUD + 404 + payload inválido.
