# Estándar de Codificación (Software - General)

[← Volver al índice](../../00-arquitectura-documentos/README.md)

## Objetivo

- Unificar estructura, nomenclatura y estilo en soluciones de software de la carrera.
- Facilitar mantenimiento, pruebas, revisión y evolución técnica.
- Evitar que cada equipo implemente criterios distintos para una misma temática.

## Alcance temático

- Aplica a desarrollo de software en general (backend, frontend, APIs, persistencia y pruebas).
- No depende del nombre de un curso; se mantiene estable por temática.
- Reglas específicas (por ejemplo, microservicios Spring Boot) se documentan en estándares complementarios.

## Convención general

- Usar nombres claros, descriptivos y consistentes.
- Mantener separación por capas o módulos según la arquitectura elegida.
- Priorizar legibilidad por sobre abreviaciones crípticas.
- Evitar duplicación de lógica y archivos sin propósito claro.

## Convención de nombres en Java

- Clases: `PascalCase`
- Métodos: `camelCase`
- Variables: `camelCase`
- Constantes: `UPPER_SNAKE_CASE`
- Paquetes: minúsculas

## Convención de nombres transversal

- Carpetas y archivos: `kebab-case` cuando aplique en proyectos web/documentales.
- Tablas y columnas SQL: `snake_case`.
- Recursos API: plural, en minúsculas y versionados.
- Entidades de dominio: singular.

## Organización mínima esperada

- `domain` o `model`
- `application` o `service`
- `infrastructure` o `repository`
- `interfaces` o `controller`
- `shared` (errores, utilidades, configuración)

## Reglas API/REST

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

## Reglas de calidad mínima

- Toda funcionalidad debe incluir validaciones básicas de entrada.
- Toda capa crítica debe tener pruebas automatizadas mínimas.
- Los errores deben ser trazables y entendibles.
- El código debe pasar revisión de pares antes de integrarse a `main`.

## Base de datos y scripts

- Toda modificación de esquema debe quedar versionada.
- Evitar cambios manuales no trazables en ambientes compartidos.
- Definir convenciones explícitas para migraciones en cada stack.

## Testing mínimo esperado

- Pruebas unitarias de lógica crítica.
- Pruebas de integración para flujos principales.
- Verificación mínima de contratos API cuando aplique.

## Logging

- Usar `Slf4j`.
- No usar `System.out.println`.
- Mantener trazabilidad con `traceId` cuando aplique.

## Estándar específico relacionado

- [Estándar de Codificación (Software - Microservicios)](estandar-codificacion-microservicios.md)

## Regla principal

La mejor convención es la que se define una sola vez, se mantiene por temática y se aplica de forma consistente en toda la línea de software.