# TASK — Cadastro de Usuário e Auditoria de Acesso

> Sprint 1 · Contas Domésticas · (colar no ClickUp)

## Premissa

- O sistema Contas Domésticas terá uma **API local** (Spring Boot / PostgreSQL) e um **app Android**
  (Kotlin / Room) que trabalham offline-first e **sincronizam** dados entre si.
- É necessário um cadastro básico de **usuários** e um mecanismo de **auditoria** que registre as
  ações (requisições) realizadas, para rastreabilidade.
- Conflitos de sincronização, por ora, são resolvidos pelo registro **mais recente** (por isso os
  campos `criado_em`/`atualizado_em`). A lógica de merge fica para uma tarefa futura.
- Autenticação JWT completa é rodada futura; nesta tarefa a segurança fica temporariamente aberta
  (permitAll) apenas para viabilizar o desenvolvimento/testes.

## Objetivo

Implementar a entidade **Usuário** e a tabela de **Auditoria** na API e espelhá-las no banco local
(Room) do app, incluindo o registro automático de cada chamada HTTP na auditoria, com cobertura por
testes automatizados.

## Especificação Funcional

- **Usuário**: `id`, `login` (único), `nome de exibição`, `senha` (armazenada com hash BCrypt) e
  campos de auditoria (`criado_em`, `criado_por`, `atualizado_em`, `atualizado_por`).
- **CRUD de usuários** via API REST (`/api/v1/usuarios`): criar, listar, buscar por id, atualizar,
  remover. A senha **nunca** é retornada.
- **Login duplicado** deve ser rejeitado (conflito).
- **Auditoria**: cada requisição HTTP tratada pela API gera um registro com `usuário`, `método HTTP`,
  `endpoint`, `status da resposta`, `endereço IP` e `data/hora`.
- **App**: mesmo modelo de dados no banco local (Room); cada chamada do app à API é registrada na
  auditoria local (via interceptor OkHttp).
- **Usuário administrador padrão** (`admin` / `admin`, exibição "Admin") disponível como seed.
- **Usuários iniciais** (seed manual, fora do versionamento): `Bruno` (Bruno Oliveira) e `Karla`
  (Karla Linhares).

## Especificação Técnica

- **API**: Java 17, Spring Boot 3.5.16, Spring Data JPA, Spring Security (temporário `permitAll` +
  `BCryptPasswordEncoder`), Bean Validation, MapStruct, Flyway.
  - `BaseEntity` (`@MappedSuperclass`, id) → `EntidadeAuditavel` (auditoria via `@EnableJpaAuditing`
    + `AuditorAware`) → `Usuario`. `Auditoria` estende apenas `BaseEntity`.
  - `AuditoriaFilter` (`OncePerRequestFilter`) grava cada requisição (ignora `/actuator`,
    `/swagger`, `/v3/api-docs`, `/error`).
  - Erros no padrão **ProblemDetail (RFC 7807)** via `@RestControllerAdvice`.
  - **Flyway**: `V1` (usuario), `V2` (auditoria), `V3` (seed admin/admin — idempotente).
- **Banco (repo db)**: scripts separados em `ddl/tables`, `ddl/primary`, `ddl/index` e o seed admin
  em `dml/inserts` (espelho do Flyway).
- **App Android**: Room (`UsuarioEntity`, `AuditoriaEntity`, DAOs, `AppDatabase`), Hilt, Retrofit +
  Moshi + OkHttp; `AuditoriaInterceptor` grava as chamadas na auditoria local.
- **Testes**: banco **H2 em memória** (profile `test`), seed de teste `admin/admin` via `data.sql`.

## Critérios de Aceite

1. É possível criar um usuário e ele é persistido com a senha em **hash BCrypt** (nunca em texto).
2. A resposta da API **não expõe** a senha.
3. Criar usuário com `login` já existente retorna **409 (conflito)**.
4. Payload inválido retorna **400** com a lista de campos inválidos (`erros`).
5. Buscar/atualizar/remover funcionam; recurso inexistente retorna **404**.
6. Campos `criado_em`/`criado_por` são preenchidos automaticamente ao criar.
7. Cada requisição HTTP gera um registro na tabela **auditoria** (método, endpoint, status, data).
8. Existe o usuário **admin/admin** (seed) no ambiente de teste e via Flyway (dev/prod).
9. O app possui o **mesmo modelo** no banco local (Room) e registra as chamadas à API na auditoria local.
10. Todos os cenários acima são cobertos por **testes automatizados** (a suíte passa).

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

## Fora de escopo (próximas tarefas)

- Autenticação/autorização JWT reais (login/registro, filtro/AuthorizationManager).
- Lógica de resolução de conflitos de sincronização.
- Telas do app (Jetpack Compose).
