# Política de Ramas y PR

[← Volver al índice](../../00-arquitectura-documentos/README.md)

## Objetivo

Establecer una forma simple y consistente de trabajar cambios en repositorios de la línea de software.

## Rama principal

- La rama estable del repositorio es `main`.
- No se trabaja directamente sobre `main`.

## Ramas para alumnos

Formato recomendado:

```text
tarea/<nombre-alumno>-<tema>
```

Para trabajos de `microservicios4`, formato sugerido:

```text
tarea/<nombre-alumno>-ms4-<tema>
```

Ejemplos:

- `tarea/ana-perez-crud-productos`
- `tarea/luis-quiroz-validacion-categorias`
- `tarea/ana-perez-ms4-ms-catalogo`

## Ramas para docentes o responsables de sesión

Formato recomendado:

```text
sesion/<numero>-<tema>
```

Ejemplos:

- `sesion/01-base-catalogo`
- `sesion/02-pruebas-y-pr`

## Tags de cierre por sesión

Formato recomendado:

```text
vs<numero>-<tema>-final
```

Ejemplos:

- `vs01-base-catalogo-final`
- `vs02-pruebas-y-pr-final`

Cuándo crear el tag:

- Después de aprobar y hacer merge del PR a `main`.
- Con pruebas mínimas ejecutadas correctamente.
- Cuando el entregable de sesión esté listo para cierre/publicación.

Flujo mínimo recomendado:

1. Validar que `main` tenga el merge final de la sesión.
2. Crear tag con formato `vs<numero>-<tema>-final`.
3. Publicar el tag en remoto.

Comandos Git (ejemplo):

```bash
git checkout main
git pull origin main
git tag vs01-base-catalogo-final
git push origin vs01-base-catalogo-final
```

## Flujo mínimo de trabajo

1. Actualizar `main`.
2. Crear rama propia.
3. Implementar cambio.
4. Ejecutar pruebas.
5. Hacer commit claro.
6. Subir rama.
7. Abrir PR hacia `main`.

## Regla para microservicios4

- El trabajo se realiza en rama propia (según estándar de nombres).
- La integración se hace por PR hacia la raíz `main`.

### Plantillas listas para usar (microservicios4)

Rama de trabajo:

```text
tarea/<nombre-alumno>-ms4-<nombre-microservicio>
```

Ejemplos:

- `tarea/juan-perez-ms4-ms-catalogo`
- `tarea/maria-lopez-ms4-ms-clientes`

Título sugerido de PR:

```text
feat(ms4): base de <nombre-microservicio> desde 01-plantilla-ms-base
```

## Mensajes de commit

Ejemplos válidos:

- `feat: agrega CRUD de productos`
- `fix: corrige validacion de categoria`
- `docs: actualiza guia de ramas`

## PR

Todo PR debe indicar:

- objetivo del cambio
- cambios principales
- artefacto de prueba
- impacto en base de datos si aplica

## Merge recomendado

- Preferir `Squash and merge` para dejar historial limpio.
- Cerrar y eliminar la rama cuando el PR ya fue integrado.