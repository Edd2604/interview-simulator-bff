# interview-simulator-bff

Backend del Simulador de Entrevistas. NestJS 12 con arquitectura hexagonal y CQRS.

@AGENTS.md

## Reglas del proyecto

Estas reglas mandan sobre la skill `nestjs-best-practices`. De la skill vale lo general (DI, errores, seguridad, validación, health checks); cuando choca con algo de acá, gana esto.

### Arquitectura hexagonal

- Carpetas por módulo: `src/modules/<module>/{domain,application,infrastructure}`.
- `domain` es TypeScript puro: no importa NestJS, Prisma ni AWS.
- Los puertos son interfaces del dominio. Se inyectan con un token (`@Inject(SESSION_REPOSITORY)`), nunca con la clase concreta.
- Los adaptadores viven en `infrastructure` e implementan los puertos. Cambiar de tecnología es cambiar un adaptador.
- Las dependencias apuntan siempre hacia el dominio.

### CQRS

- `@nestjs/cqrs`: un handler por comando o consulta.
- Los comandos escriben y pasan por las entidades del dominio.
- Las consultas solo leen, directo con Prisma, y devuelven DTOs. Nunca cambian estado.

### Stack

- Base de datos: Prisma + PostgreSQL. No TypeORM.
- Tests: Vitest. Mocks con `vi.fn()`, nunca `jest.fn()`.
- ESM: las importaciones relativas terminan en `.js`.
- Documentación: Swagger (`@nestjs/swagger`) y health checks (`@nestjs/terminus`).

### Código

- Siempre en inglés: carpetas, clases, variables, rutas y tablas.

### Commits

- Una línea: `tipo: descripción` (`feat`, `fix`, `refactor`, `chore`, `docs`, `test`).
- Sin `Co-Authored-By` ni ninguna firma de Claude.
