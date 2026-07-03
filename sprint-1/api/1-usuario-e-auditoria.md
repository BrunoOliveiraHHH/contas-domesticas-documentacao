# TASK — Usuário e Auditoria · API

> Sprint 1 · Contas Domésticas · Projeto API · Usuário + Auditoria
> (colar no ClickUp) · Modelo-base para as próximas tarefas de API

## Premissa

- A **API local** (Spring Boot / PostgreSQL) é o ponto de sincronização dos dados entre as instâncias
  (app nos dois celulares).
- É necessário um cadastro básico de **usuários** e um mecanismo de **auditoria** que registre cada
  requisição, para rastreabilidade.
- Conflitos de sincronização, por ora, são resolvidos pelo registro **mais recente** (campos
  `criado_em`/`atualizado_em`). Merge fica para tarefa futura.
- Autenticação JWT completa é rodada futura; aqui a segurança fica temporariamente aberta (`permitAll`)
  apenas para viabilizar desenvolvimento/testes.

## Objetivo

Implementar a entidade **Usuário** e a tabela de **Auditoria** na API, com registro automático de cada
chamada HTTP e cobertura por testes automatizados.

## Especificação Funcional

- **Usuário**: `id`, `login` (único), `nome de exibição`, `senha` (hash BCrypt) e campos de auditoria
  (`criado_em`, `criado_por`, `atualizado_em`, `atualizado_por`).
- **CRUD** via REST (`/api/v1/usuarios`): criar, listar, buscar por id, atualizar, remover. A senha
  **nunca** é retornada.
- **Login duplicado** é rejeitado (conflito).
- **Auditoria**: cada requisição HTTP tratada gera um registro com `usuário`, `método HTTP`,
  `endpoint`, `status da resposta`, `endereço IP` e `data/hora`.
- **Usuário administrador padrão** (`admin` / `admin`, exibição "Admin") disponível como seed.

## Especificação Técnica

- **Stack**: Java 17, Spring Boot 3.5.16, Spring Data JPA, Spring Security (temporário `permitAll` +
  `BCryptPasswordEncoder`), Bean Validation, MapStruct, Flyway.
- **Domínio (reutilizável)**: `BaseEntity` (`@MappedSuperclass`, id) → `EntidadeAuditavel` (auditoria
  via `@EnableJpaAuditing` + `AuditorAware`) → `Usuario`. `Auditoria` estende apenas `BaseEntity`.
- **Auditoria automática**: `AuditoriaFilter` (`OncePerRequestFilter`) grava cada requisição; ignora
  `/actuator`, `/swagger`, `/v3/api-docs`, `/error`; try/catch para nunca quebrar a request.
- **Erros**: padrão **ProblemDetail (RFC 7807)** via `@RestControllerAdvice`
  (`@Order(HIGHEST_PRECEDENCE)` para preceder o handler padrão).
- **Flyway** (fonte de verdade): `V1` (usuario), `V2` (auditoria), `V3` (seed admin/admin —
  idempotente).
- **Testes**: banco **H2 em memória** (profile `test`, forçado no surefire), seed de teste `admin/admin`
  via `data.sql`.

## Critérios de Aceite

1. Criar usuário persiste a senha em **hash BCrypt** (nunca em texto).
2. A resposta da API **não expõe** a senha.
3. `login` já existente retorna **409 (conflito)**.
4. Payload inválido retorna **400** com a lista de campos (`erros`).
5. Buscar/atualizar/remover funcionam; recurso inexistente retorna **404**.
6. `criado_em`/`criado_por` são preenchidos automaticamente ao criar.
7. Cada requisição HTTP gera registro em **auditoria** (método, endpoint, status, data).
8. Existe o usuário **admin/admin** (seed) no ambiente de teste e via Flyway.
9. Todos os cenários são cobertos por **testes automatizados** (a suíte passa).

## Cenários de Teste (automatizados)

| # | Cenário | Resultado esperado | Coberto por |
|---|---------|--------------------|-------------|
| 1 | Criar usuário válido | 201; retorna id; sem senha; `criadoEm` preenchido | `UsuarioControllerIntegrationTest.deveCriarUsuarioSemExporSenha` |
| 2 | Senha é codificada (BCrypt) | senha salva ≠ senha original | `UsuarioServiceTest.deveCriarUsuarioCodificandoASenha` |
| 3 | Login duplicado | 409 | `...deveRejeitarLoginDuplicadoComConflito` / `UsuarioServiceTest.naoDeveCriarUsuarioComLoginDuplicado` |
| 4 | Payload inválido | 400 com `erros` | `...deveRejeitarPayloadInvalidoComBadRequest` |
| 5 | Buscar / atualizar / remover | 200 / 200 / 204 e depois 404 | `...deveBuscarAtualizarERemover` |
| 6 | Recurso inexistente | 404 (ProblemDetail) | `...deveRetornar404ParaUsuarioInexistente` / `UsuarioServiceTest.deveLancarQuandoUsuarioNaoEncontrado` |
| 7 | Auditoria da requisição | registro gravado (método/endpoint/status) | `...deveRegistrarAuditoriaDaRequisicao` |
| 8 | Seed admin no ambiente de teste | usuário `admin` existe; BCrypt confere | `...seedDeTesteDeveConterUsuarioAdminComSenhaBcrypt` |
| 9 | Auditoria de persistência (repositório) | registro persistido | `AuditoriaRepositoryTest.devePersistirRegistroDeAuditoria` |
| 10 | Auditoria automática ao persistir usuário | `criado_em`/`criado_por` preenchidos | `UsuarioRepositoryTest.devePersistirUsuarioComCamposDeAuditoriaPreenchidos` |

**Status:** suíte executada com `./mvnw verify` (profile `test`, H2) — **14/14 testes verdes**.

## Fora de escopo (próximas tarefas de API)

Ver `PLANO-api.md` (raiz do workspace): Autenticação JWT, Carteiras, Cadastros base, Parâmetros,
Receitas/Despesas, Compras, Investimentos, Relatórios, Sincronização.
