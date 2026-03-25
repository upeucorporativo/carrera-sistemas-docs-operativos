# Prompt para Alumnos

[← Volver al índice](../../00-arquitectura-documentos/README.md)

## Uso

Este prompt sirve para clonar la base `catalogo` y convertirla en un nuevo microservicio manteniendo el estándar de la línea de software.

Referencia obligatoria de plantilla:
- URL: `https://github.com/261dist/catalogo/tree/01-plantilla-ms-base`
- Rama base de plantilla: `01-plantilla-ms-base`

Flujo de ramas y PR:
- Crear rama de trabajo según estándar vigente de nombres en `04-estandares-operativos/software/politica-ramas-pr.md`.
- Mantener PR de integración hacia la rama raíz `main` del repositorio donde se implementa el microservicio.

Plantilla rápida (copiar/pegar):

```text
Rama de trabajo: tarea/<autor>-ms4-<nombre-microservicio>
Rama origen plantilla: 01-plantilla-ms-base
Rama destino PR: main
Título PR sugerido: feat(ms4): base de <nombre-microservicio> desde 01-plantilla-ms-base
```

## Prompt base

Quiero crear un nuevo microservicio Spring Boot a partir de la plantilla base `catalogo`, siguiendo el estándar de la línea de software.

Contexto:
- Proyecto base: `catalogo`
- URL base: `https://github.com/261dist/catalogo/tree/01-plantilla-ms-base`
- Rama base: `01-plantilla-ms-base`
- Nuevo microservicio: `[NOMBRE_MS]`
- Paquete base: `com.upeu.[NOMBRE_MS]`
- Entidad principal: `[NOMBRE_ENTIDAD]`
- Tabla SQL: `[NOMBRE_TABLA]`
- Endpoint base: `/api/v1/[RECURSO_PLURAL]`
- Rama de trabajo: `[RAMA_SEGUN_ESTANDAR]`
- Rama destino PR: `main`

Tareas que debes ejecutar:
1. Crear una nueva copia de la plantilla base en el repositorio del nuevo microservicio.
	- usar como fuente la rama `01-plantilla-ms-base`.
2. Renombrar paquete, clases y referencias de `catalogo/Categoria` a `[NOMBRE_MS]/[NOMBRE_ENTIDAD]`.
3. Crear o ajustar `entity`, `dto`, `mapper`, `repository`, `service`, `controller` y pruebas.
4. Ajustar `pom.xml` al nuevo microservicio.
5. Ajustar `application.yml`, `application-dev.yml` y `application-prod.yml`.
6. Crear migración Flyway inicial.
7. Ajustar Docker y puertos sin conflicto.
8. Actualizar `README.md` con nombre, puertos y endpoints correctos.
9. No copiar documentación operativa transversal dentro del microservicio.
10. Ejecutar pruebas y reportar el resultado.
11. Abrir PR desde `[RAMA_SEGUN_ESTANDAR]` hacia `main`.

Reglas obligatorias:
- No editar migraciones Flyway ya ejecutadas en entornos compartidos.
- Mantener arquitectura por capas.
- Usar nombres Java claros.
- Mantener tablas en plural y entidades en singular.

Salida esperada:
- archivos modificados
- puertos finales
- resultado de pruebas