# Política de Ramas y PR

[← Volver al índice](../../00-arquitectura-documentos/README.md)

## Objetivo

Establecer una forma simple y consistente de trabajar cambios en repositorios de la línea de software.

## Rama principal

- La rama estable del repositorio es `main`.
- No se trabaja directamente sobre `main`.

## Regla común (aplica a todos)

- Todo cambio se desarrolla en rama de trabajo.
- Toda integración se realiza por PR hacia `main`.
- `main` queda reservada para integración estable.

## Formato de ramas de trabajo (común)

### Ramas de trabajo (alumnos)

Formato:

```text
tarea/<autor>-<tema>
```

Para `microservicios4`, formato sugerido:

```text
tarea/<autor>-ms4-<tema>
```

Ejemplos:

- `tarea/ana-perez-crud-productos`
- `tarea/luis-quiroz-validacion-categorias`
- `tarea/ana-perez-ms4-ms-catalogo`

### Ramas de sesión (docentes)

Formato:

```text
sesion/<numero>-<tema>
```

Ejemplo:

```bash
git checkout -b sesion/01-arquitectura-base-ms
```

## Flujo mínimo de trabajo

1. Sincronizar `main` cuando la tarea es nueva.
2. Crear rama propia de trabajo.
3. Implementar cambio.
4. Ejecutar pruebas.
5. Hacer commit claro.
6. Subir rama.
7. Abrir PR hacia `main`.

Comandos Git (flujo general):

```bash
# 1) Tarea nueva: actualizar main
git checkout main
git pull origin main

# 2) Crear rama propia
git checkout -b tarea/<autor>-ms4-<tema>

# 3) Implementar cambio
# (editar archivos)

# 4) Ejecutar pruebas
mvn test

# 5) Commit claro
git add .
git commit -m "feat(ms4): <descripcion-corta>"

# 6) Subir rama
git push -u origin tarea/<autor>-ms4-<tema>

# 7) Abrir PR hacia main (desde GitHub)
```

Comandos Git (si continúas en tu misma rama):

```bash
git checkout tarea/<autor>-ms4-<tema>
git pull origin tarea/<autor>-ms4-<tema>
mvn test
git add .
git commit -m "feat(ms4): <descripcion-corta>"
git push origin tarea/<autor>-ms4-<tema>
```

## Primera publicación desde local (bootstrap)

Cuando un proyecto nace local y todavía no existe en GitHub, usar este flujo para cumplir la política.

### ¿Cuándo se crea `main`?

- `main` se crea al crear el repositorio en GitHub (si inicias con README), o
- en el primer push al remoto desde la rama local `main`.

### Regla práctica

- Se permite un **push inicial de bootstrap** a `main` solo para crear la línea base del repositorio.
- Desde ese punto, todo cambio de desarrollo va en rama propia y entra por PR a `main`.

### Flujo recomendado (proyecto ya hecho en local)

```bash
# 1) En local: dejar la rama base como main
git branch -M main

# 2) Crear repo vacío en GitHub y vincular remoto
git remote add origin <url-del-repo>

# 3) Push inicial (bootstrap) para crear main remoto
git push -u origin main

# 4) Crear rama de trabajo según estándar
git checkout -b tarea/<autor>-ms4-<tema>

# 5) Continuar desarrollo en tu rama
git add .
git commit -m "feat(ms4): <descripcion-corta>"
git push -u origin tarea/<autor>-ms4-<tema>
```

### Flujo recomendado (repo creado primero en GitHub)

```bash
# 1) Clonar (main ya existe)
git clone <url-del-repo>
cd <repo>

# 2) Crear rama de trabajo
git checkout -b tarea/<autor>-ms4-<tema>

# 3) Trabajar y subir rama
git add .
git commit -m "feat(ms4): <descripcion-corta>"
git push -u origin tarea/<autor>-ms4-<tema>
```

### Regla final

- No hacer desarrollo continuo en `main`; usar siempre rama propia + PR.

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

## Convención específica para microservicios4

- Mantener el prefijo `ms4` en el nombre de rama.
- Integrar siempre por PR a `main`.

Plantillas listas para usar:

Rama de trabajo:

```text
tarea/<autor>-ms4-<nombre-microservicio>
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
- estrategia de merge esperada: `Squash and merge`

Plantilla breve de descripción de PR (copiar/pegar):

```text
## Objetivo del cambio
<describir objetivo>

## Cambios principales
- <cambio 1>
- <cambio 2>

## Artefacto de prueba
- <captura, log o evidencia>

## Impacto en base de datos
- [ ] No aplica
- [ ] Sí aplica: <describir migración/impacto>

## Estrategia de merge esperada
- Squash and merge
```

## Merge recomendado

- Preferir `Squash and merge` para dejar historial limpio.
- Cerrar y eliminar la rama cuando el PR ya fue integrado.