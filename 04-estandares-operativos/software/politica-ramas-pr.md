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

Ejemplos:

- `tarea/ana-perez-crud-productos`
- `tarea/luis-quiroz-validacion-categorias`

## Ramas para docentes o responsables de sesión

Formato recomendado:

```text
sesion/<numero>-<tema>
```

Ejemplos:

- `sesion/01-base-catalogo`
- `sesion/02-pruebas-y-pr`

## Flujo mínimo de trabajo

1. Actualizar `main`.
2. Crear rama propia.
3. Implementar cambio.
4. Ejecutar pruebas.
5. Hacer commit claro.
6. Subir rama.
7. Abrir PR hacia `main`.

## Mensajes de commit

Ejemplos válidos:

- `feat: agrega CRUD de productos`
- `fix: corrige validacion de categoria`
- `docs: actualiza guia de ramas`

## PR

Todo PR debe indicar:

- objetivo del cambio
- cambios principales
- evidencia de prueba
- impacto en base de datos si aplica

## Merge recomendado

- Preferir `Squash and merge` para dejar historial limpio.
- Cerrar y eliminar la rama cuando el PR ya fue integrado.