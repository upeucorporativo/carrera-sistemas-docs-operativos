# Prompt para Alumnos

[← Volver al índice](../../00-arquitectura-documentos/README.md)

## Uso

Este prompt sirve para clonar la base `catalogo` y convertirla en un nuevo microservicio manteniendo el estándar de la línea de software.

## Prompt base

Quiero crear un nuevo microservicio Spring Boot a partir de la plantilla base `catalogo`, siguiendo el estándar de la línea de software.

Contexto:
- Proyecto base: `catalogo`
- Nuevo microservicio: `[NOMBRE_MS]`
- Paquete base: `com.upeu.[NOMBRE_MS]`
- Entidad principal: `[NOMBRE_ENTIDAD]`
- Tabla SQL: `[NOMBRE_TABLA]`
- Endpoint base: `/api/v1/[RECURSO_PLURAL]`

Tareas que debes ejecutar:
1. Crear una nueva copia de la plantilla base en el repositorio del nuevo microservicio.
2. Renombrar paquete, clases y referencias de `catalogo/Categoria` a `[NOMBRE_MS]/[NOMBRE_ENTIDAD]`.
3. Crear o ajustar `entity`, `dto`, `mapper`, `repository`, `service`, `controller` y pruebas.
4. Ajustar `pom.xml` al nuevo microservicio.
5. Ajustar `application.yml`, `application-dev.yml` y `application-prod.yml`.
6. Crear migración Flyway inicial.
7. Ajustar Docker y puertos sin conflicto.
8. Actualizar `README.md` con nombre, puertos y endpoints correctos.
9. No copiar documentación operativa transversal dentro del microservicio.
10. Ejecutar pruebas y reportar el resultado.

Reglas obligatorias:
- No editar migraciones Flyway ya ejecutadas en entornos compartidos.
- Mantener arquitectura por capas.
- Usar nombres Java claros.
- Mantener tablas en plural y entidades en singular.

Salida esperada:
- archivos modificados
- puertos finales
- resultado de pruebas