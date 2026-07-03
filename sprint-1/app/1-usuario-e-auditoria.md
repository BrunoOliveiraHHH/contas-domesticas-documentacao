# TASK — Usuário e Auditoria · App

> Sprint 1 · Contas Domésticas · Projeto App · Usuário + Auditoria
> (colar no ClickUp) · Modelo-base para as próximas tarefas de App

## Premissa

- O app Android é **offline-first**: mantém os dados no banco local (Room) e **sincroniza** com a API.
- Precisa do mesmo modelo de **usuário** e **auditoria** local, registrando cada chamada feita à API
  para rastreabilidade no dispositivo.
- Conflitos de sincronização, por ora, resolvidos pelo **mais recente**; merge fica para tarefa
  futura.

## Objetivo

Espelhar **Usuário** e **Auditoria** no banco local (Room) e registrar automaticamente cada chamada à
API na auditoria local, via interceptor OkHttp.

## Especificação Funcional

- **Mesmo modelo de dados** no banco local (Room): `Usuario` e `Auditoria`.
- Cada chamada do app à API é **registrada na auditoria local** (método, endpoint, status, data/hora).
- Base para o futuro fluxo de login e sincronização (a API já expõe `/api/v1/usuarios`).

## Especificação Técnica

- **Stack**: Kotlin, Room 2.6.1, Hilt, Retrofit 2.11 + Moshi + OkHttp; UI em Compose (infra pronta,
  telas em rodada futura).
- **Room**: `UsuarioEntity` (`@Entity("usuario")`, login índice único, timestamps `Long`),
  `AuditoriaEntity` (`@Entity("auditoria")`); DAOs (`UsuarioDao`, `AuditoriaDao` com
  `inserirBloqueante` não-suspend para o interceptor); `AppDatabase` (version 1);
  `DatabaseModule` (Hilt, `fallbackToDestructiveMigration`).
- **Rede**: `UsuarioApi` (Retrofit), `UsuarioDto`/`UsuarioRequestDto`, `NetworkModule`
  (OkHttp com `AuditoriaInterceptor` + `HttpLoggingInterceptor`, Retrofit com `BuildConfig.API_BASE_URL`).
- **AuditoriaInterceptor** (`okhttp3.Interceptor`, `@Inject AuditoriaDao`): prossegue a requisição e
  grava o registro no Room em try/catch (nunca quebra a chamada).
- Removido o placeholder anterior (`ContaEntity`/`ContaDao`).

## Critérios de Aceite

1. O app possui o **mesmo modelo** (Room) de `Usuario` e `Auditoria` da API.
2. Cada chamada à API gera um registro na **auditoria local**.
3. O `AuditoriaInterceptor` **não interrompe** a requisição em caso de falha ao gravar.
4. `AppDatabase`, DAOs e módulos Hilt compilam e são injetáveis.
5. Sem referências ao antigo `Conta*`.

## Verificação

- **Estática** neste ambiente (sem Gradle/SDK): revisão de Room/Hilt/Retrofit e das referências do
  version catalog.
- **Aceite final**: build no **Android Studio** e, futuramente, testes instrumentados (Room/DAO e
  interceptor) — ver item 14 do `PLANO-app.md`.

## Fora de escopo (próximas tarefas de App)

Ver `PLANO-app.md` (raiz do workspace): Fundação Compose, Login, Carteiras, Cadastros, Configuração,
Receitas/Despesas, Compras, Investimentos, Calculadoras, Dashboard, Sincronização, testes
instrumentados.
