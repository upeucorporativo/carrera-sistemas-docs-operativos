# Estándar de Codificación para Microservicios Spring Boot

[← Volver al índice](../../00-arquitectura-documentos/README.md)

## Objetivo

- Unificar estructura, nomenclatura y estilo en los microservicios de la línea de software.
- Facilitar mantenimiento, pruebas, revisión y escalabilidad.
- Evitar que cada equipo implemente criterios distintos para el mismo tipo de solución.

## Convención general

- Java con nombres claros y completos.
- SQL con tablas en plural y columnas en `snake_case`.
- API REST con recursos en plural y versionados.
- Entidades en singular.

## Convención de nombres en Java

- Clases: `PascalCase`
- Métodos: `camelCase`
- Variables: `camelCase`
- Constantes: `UPPER_SNAKE_CASE`
- Paquetes: minúsculas

## Capas mínimas esperadas

- `controller`
- `service`
- `service.impl`
- `repository`
- `entity`
- `dto`
- `mapper`
- `exception`
- `config`

## Reglas REST

- Endpoints en plural.
- Versionado desde el inicio: `/api/v1/<recurso>`.
- Usar sustantivos, no verbos.

Ejemplos:

- `GET /api/v1/categorias`
- `POST /api/v1/productos`
- `PUT /api/v1/clientes/{id}`

## DTOs y entidades

- Entidad: singular.
- DTO de entrada: `NombreRequest`.
- DTO de salida: `NombreResponse`.
- No exponer entidades directamente en contratos REST.

## Base de datos y migraciones

- `dev`: puede usar `ddl-auto: update` con fines de aprendizaje.
- `prod`: debe usar Flyway y `ddl-auto: validate`.
- Toda modificación de esquema debe quedar en SQL versionado.
- No se reescriben migraciones ya ejecutadas en ambientes compartidos.

## Testing mínimo esperado

- Test de contexto.
- Test de mapper.
- Test de service.
- Test de controller.

## Logging

- Usar `Slf4j`.
- No usar `System.out.println`.
- Mantener trazabilidad con `traceId` cuando aplique.

## Regla principal

La mejor convención es la que se define una sola vez y se respeta en todos los microservicios de la línea de software.