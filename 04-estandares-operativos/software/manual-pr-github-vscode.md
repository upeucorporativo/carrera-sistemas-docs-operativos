# Manual de Pull Request (GitHub Web y VS Code)

[← Volver al índice](../../00-arquitectura-documentos/README.md)

## Objetivo

Guiar paso a paso la creación, revisión y cierre de Pull Request (PR) usando:

- GitHub Web
- Visual Studio Code (extensión de PR)

Este manual complementa la [Política de ramas y PR](politica-ramas-pr.md).

## Alcance

- Aplica a alumnos y docentes.
- Aplica a ramas de trabajo (`tarea/...`) y de sesión (`sesion/...`).
- La rama base de integración es `main`.

## Requisitos previos

1. Tener permisos sobre el repositorio en GitHub.
2. Tener una rama subida al remoto:
   - ejemplo alumno: `tarea/ana-perez-ms4-ms-catalogo`
   - ejemplo docente: `sesion/01-arquitectura-base-ms`
3. Tener cambios con commit en esa rama.

---

## Flujo A: Crear PR desde GitHub Web

### 1) Abrir comparación

- Entra al repositorio en GitHub.
- Si aparece el banner amarillo de tu rama, selecciona `Compare & pull request`.
- Si no aparece, entra a `Pull requests` → `New pull request`.

### 2) Verificar ramas

- `base`: `main`
- `compare`: tu rama de trabajo (`tarea/...` o `sesion/...`)

### 3) Completar título y descripción

Título sugerido (ejemplos):

- `feat(ms4): base de ms-catalogo`
- `feat(sesion-01): arquitectura base ms`

Descripción sugerida (copiar/pegar):

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

### 4) Crear PR

- Presiona `Create pull request`.
- Agrega reviewers si corresponde.

### 5) Resolver comentarios (si hay)

- Responde comentarios del PR.
- Ajusta código en tu misma rama y vuelve a hacer push.
- El PR se actualiza automáticamente.

### 6) Integrar PR

- Cuando esté aprobado y sin conflictos, usar `Squash and merge`.
- Eliminar rama remota al finalizar.

### 7) Post-merge obligatorio con Squash

Regla de oro:

- Con `Squash and merge`, la rama fuente queda "huérfana" respecto al historial.
- No se debe seguir trabajando en esa misma rama.
- Se debe borrar y crear una rama nueva desde la rama destino actualizada.

Comandos de referencia (ejemplo real aplicado):

```bash
# 1) Borrar rama vieja
git branch -d sesion/01-arquitectura-base-ms
git push origin --delete sesion/01-arquitectura-base-ms

# 2) Actualizar rama destino y crear nueva rama
git fetch origin
git checkout sesion/01-arquitectura-base-ms
git pull
git checkout -b tarea/02-siguiente-tarea
```

Variación equivalente para ramas `tarea/...`:

```bash
git branch -d tarea/01-ms-producto
git push origin --delete tarea/01-ms-producto
```

Adaptar nombres de ramas según la sesión/proyecto.

### Ejemplo concreto (caso real sesión 01)

Escenario aplicado:

- Rama de trabajo: `sesion/01-arquitectura-base-ms`
- Rama base: `main`
- PR: `feat: arquitectura base microservicio catalogo`

Paso a paso ejecutado:

1. Clonar el repositorio y entrar al proyecto:

```powershell
PS C:\ms1\ProyectosMS2026\services> git clone https://github.com/261dist/catalogo.git
PS C:\ms1\ProyectosMS2026\services> cd .\catalogo\
PS C:\ms1\ProyectosMS2026\services\catalogo> code .
```

2. Verificar rama base y crear rama de sesión:

```powershell
PS C:\ms1\ProyectosMS2026\services\catalogo> git branch
* main
PS C:\ms1\ProyectosMS2026\services\catalogo> git checkout -b sesion/01-arquitectura-base-ms
PS C:\ms1\ProyectosMS2026\services\catalogo> git branch
  main
* sesion/01-arquitectura-base-ms
```

3. Realizar el trabajo en la rama `sesion/01-arquitectura-base-ms`.

4. Preparar commit y subir la rama:

```powershell
PS C:\ms1\ProyectosMS2026\services\catalogo> git add .
PS C:\ms1\ProyectosMS2026\services\catalogo> git commit -m "feat: arquitectura base microservicio catalogo"
PS C:\ms1\ProyectosMS2026\services\catalogo> git push -u origin sesion/01-arquitectura-base-ms
```

5. Crear PR con `base: main` y `compare: sesion/01-arquitectura-base-ms`.
6. Completar descripción de PR con objetivo, cambios, evidencia e impacto BD.
7. Verificar estado: `No conflicts with base branch`.
8. Abrir menú de merge y elegir:
   - `Squash and merge` (inglés), o
   - `Aplastar y fusionar` (español).
9. Confirmar en la pantalla final:
   - `Confirm squash and merge`.
10. Resultado esperado:
   - `Pull request successfully merged and closed`.
11. Paso opcional de limpieza:
   - `Delete branch` en GitHub o borrado posterior por comando.

Comandos de cierre local usados después del merge:

```bash
git checkout main
git pull origin main
git branch -d sesion/01-arquitectura-base-ms
git fetch --prune
```

Tag de cierre de sesión (opcional, desde `main`):

```bash
git tag vs01-arquitectura-base-ms-final
git push origin vs01-arquitectura-base-ms-final
```

Validación visual en GitHub (resultado esperado):

- En el selector de `Branches / Tags` debe aparecer el tag `vs01-arquitectura-base-ms-final`.
- En la cabecera del repositorio debe verse `1 Tag` (o el total actualizado de tags).

Comando de verificación local recomendado:

```bash
git show vs01-arquitectura-base-ms-final --no-patch --oneline
```

Bloque para evidencia de captura (agregar imagen cuando esté disponible en el repo):

```text
Captura sugerida: resultado final del tag creado
Vista esperada: lista de tags mostrando `vs01-arquitectura-base-ms-final`
```

Referencia complementaria externa:

- Documento de apoyo con comandos y capturas: https://docs.google.com/document/d/1ARddsiI2b8iX2T2AldTN3n_SLq0aYjbDHAxkU_JSNGQ/edit?usp=sharing

---

## Flujo B: Crear PR desde VS Code

### 1) Instalar extensión

- Instala `GitHub Pull Requests and Issues` (`GitHub.vscode-pull-request-github`).

### 2) Preparar rama

En Source Control:

- Verifica que estés en tu rama (`tarea/...` o `sesion/...`).
- Confirma que no haya cambios pendientes sin commit.
- Haz push si aún no existe en remoto.

### 3) Crear PR

- Abre paleta de comandos (`Ctrl+Shift+P`).
- Ejecuta: `GitHub Pull Requests: Create Pull Request`.
- Selecciona:
  - base: `main`
  - compare: tu rama
- Completa título y descripción.
- Confirma creación.

### 4) Gestionar PR desde VS Code

- Revisar comentarios del PR.
- Aplicar cambios y hacer nuevos commits/push.
- Confirmar estado de checks.

### 5) Merge

- Si la política del repositorio lo permite desde VS Code, completar merge.
- Si no, abrir PR en GitHub Web y usar `Squash and merge`.

---

## Conflictos: cómo resolverlos

Nota importante:

- La extensión `GitHub Pull Requests and Issues` sirve para crear, revisar y gestionar PR.
- No cumple el mismo rol que una herramienta visual especializada de merge como `P4Merge`.
- En VS Code, el equivalente más cercano a un resolvedor visual es el editor de merge integrado (`Merge Editor`).

## Opción 1: Resolver en GitHub Web

Cuando GitHub muestra `This branch has conflicts that must be resolved`:

1. Click en `Resolve conflicts`.
2. Edita bloques con marcadores:
   - `<<<<<<< HEAD`
   - `=======`
   - `>>>>>>> tu-rama`
3. Deja solo el contenido final correcto.
4. Elimina marcadores.
5. `Mark as resolved` en cada archivo.
6. `Commit merge`.

## Opción 2: Resolver localmente con Git

```bash
git checkout <tu-rama>
git pull origin main
# resolver conflictos en archivos
git add .
git commit -m "chore: resuelve conflictos con main"
git push origin <tu-rama>
```

El PR se actualiza automáticamente.

### Material complementario recomendado

- GitHub Docs: resolver conflictos directamente en GitHub Web
   - https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/addressing-merge-conflicts/resolving-a-merge-conflict-on-github
- GitHub Docs: resolver conflictos por línea de comandos
   - https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/addressing-merge-conflicts/resolving-a-merge-conflict-using-the-command-line
- VS Code Docs: control de código fuente y resolución de conflictos con Merge Editor
   - https://code.visualstudio.com/docs/sourcecontrol/merge-conflicts
- VS Code Docs: trabajar con GitHub Pull Requests and Issues
   - https://code.visualstudio.com/docs/sourcecontrol/github

### Qué herramienta usar según el caso

- `GitHub Web`:
   - cuando el conflicto es simple
   - cuando solo necesitas resolver pocas líneas
   - cuando no estás en tu equipo local
- `VS Code Merge Editor`:
   - cuando quieres resolución visual dentro del editor
   - cuando el conflicto afecta varios archivos de texto
   - cuando necesitas revisar cambios con más contexto
- `Terminal Git`:
   - cuando GitHub no permite resolver el conflicto en la web
   - cuando necesitas control fino del flujo Git
   - cuando trabajas en repositorios con políticas o validaciones más estrictas
- `P4Merge` u otra herramienta externa:
   - cuando prefieres una interfaz visual especializada de comparación
   - cuando ya tienes una herramienta de merge adoptada por el equipo
   - cuando el conflicto es grande y quieres una vista dedicada fuera del editor

---

## Checklist rápido antes de hacer merge

- [ ] PR apunta a `main`.
- [ ] La rama de comparación es la correcta (`tarea/...` o `sesion/...`).
- [ ] Título y descripción están completos.
- [ ] Pruebas mínimas ejecutadas.
- [ ] Sin conflictos pendientes.
- [ ] Estrategia seleccionada: `Squash and merge`.

## Checklist rápido después de hacer merge (si fue Squash)

- [ ] Rama vieja borrada en local (`git branch -d <rama>`).
- [ ] Rama vieja borrada en remoto (`git push origin --delete <rama>`).
- [ ] Rama destino actualizada (`git fetch` + `git checkout <destino>` + `git pull`).
- [ ] Nueva rama creada para la siguiente tarea (`git checkout -b <rama-nueva>`).

---

## Troubleshooting rápido

### No aparece botón para crear PR

- Verifica que la rama esté subida (`git push -u origin <rama>`).
- Confirma que `base` y `compare` sean diferentes.

### El PR muestra archivos que no quiero incluir

- Revisa commits en tu rama.
- Si incluiste cambios no deseados, corrige en la misma rama y vuelve a push.

### No puedes hacer merge

- Revisa reglas de protección de rama (reviews/checks requeridos).
- Completa los requisitos y vuelve a intentar.

---

## Evidencia de participación del equipo (rúbrica)

Eliminar la rama después del merge **no borra** la trazabilidad del trabajo.

La evidencia queda en:

- PR creados por cada integrante.
- Commits asociados al PR.
- Comentarios y revisiones en PR de otros integrantes.
- Historial de actividad en el repositorio.

### Dónde obtener reportes en GitHub

- Pull requests por persona: filtrar por `author:<usuario>`.
- Revisiones realizadas por persona: filtrar por `reviewed-by:<usuario>`.
- Comentarios por persona: filtrar por `commenter:<usuario>`.
- Contribuciones generales: `Insights` → `Contributors`.

### Evidencia mínima sugerida por integrante

- 1 PR propio mergeado.
- 1 revisión o comentario técnico en PR de otra persona.
- 1 evidencia técnica en su PR (captura, log o prueba).

### Plantilla de reporte por integrante (copiar/pegar)

```text
## Reporte de participación - <nombre integrante>

- Usuario GitHub: <usuario>
- Sprint/Sesión: <sesion>

### 1) PR propios
- PR #<numero>: <titulo> - <url>
- Estado: <merged/open/closed>

### 2) Revisiones o comentarios en PR de equipo
- PR #<numero>: <tipo: review/comment> - <url>

### 3) Evidencia técnica adjunta
- Tipo: <captura/log/test>
- Ubicación: <url del comentario, PR o artifact>

### 4) Resumen de aporte
- <descripcion breve del aporte técnico realizado>
```

---

## Anexo sugerido de capturas para este manual

Para reforzar la guía en clases, adjuntar estas capturas por cada flujo:

- pantalla de `Compare & pull request`
- validación `base/main` vs `compare/<rama>`
- selector de estrategia de merge (`Create merge commit`, `Squash and merge`, `Rebase and merge`)
- pantalla de confirmación `Confirm squash and merge`
- resultado `Pull request successfully merged and closed`
- verificación de tag en GitHub (`1 Tag` + `vs01-arquitectura-base-ms-final`)

Sugerencia operativa: guardar capturas por sesión en una carpeta del curso y enlazarlas desde este manual en futuras iteraciones.

---

## Próximas variantes de este manual

Este documento se extenderá con flujos equivalentes para:

- IntelliJ IDEA
- Eclipse
- Otros clientes Git

Mientras no se publiquen esas variantes, usar este manual como base oficial.
