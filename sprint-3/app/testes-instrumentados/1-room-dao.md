# Tarefa — Testes instrumentados: Room/DAO · App
> Sprint 3 (05/08–19/08/2026) · Bloco: Testes instrumentados · Passo 1/3 · Depende: entidades Room

## O que fazer
Validar a persistência local.

## Passo a passo
1. `@RunWith(AndroidJUnit4)` + Room in-memory; CRUD e queries dos DAOs.

## Onde mexer
- `androidTest/.../dao/*`

## Critério de pronto (DoD)
- [ ] DAOs cobertos; migrações testadas

## Como testar
`./gradlew connectedCheck` (device/emulador).
