# Convenciones del proyecto

## Idioma
Responde y documenta en español.

## Entorno
Windows con PowerShell: no uses `&&` para encadenar comandos; usa `;`.

## Specs
Las especificaciones viven en `specs/<funcionalidad>/` y cada una tiene tres archivos:

| Archivo | Contenido |
|---|---|
| `requirements.md` | Qué debe hacer: historias de usuario y criterios de aceptación numerados (`1.1`, `1.2`, `2.1`…). |
| `design.md` | Cómo se construye: componentes, interfaces, manejo de errores y estrategia de pruebas. |
| `tasks.md` | Tareas con casillas `[ ]`/`[x]`; cada una cita los requisitos que cubre (`_Requisitos: 1.1, 1.3_`). |

Reglas:
- `specs/ejemplo/` es solo una plantilla; para una funcionalidad nueva, copia esa carpeta y renómbrala.
- Numera los requisitos y haz que cada tarea los cite, para poder rastrearlos.
- No marques una tarea como `[x]` hasta que `task-verificator` la haya verificado con veredicto CUMPLE.
- No cambies requisitos ni diseño para que una tarea "pase"; si la spec debe cambiar, avisa al usuario primero.

## Subagentes (`.claude/agents/`)
- `git-helper`: tareas de Git (commits, ramas, conflictos, historial). Pide confirmación antes de operaciones destructivas.
- `task-verificator`: verifica una tarea de una spec contra requisitos y diseño, corre las pruebas y emite un veredicto. Solo lectura. Úsalo cada vez que se termine de implementar una tarea.

## Git
- Mensajes de commit en español, en imperativo, máximo 72 caracteres en el resumen.
- No hagas `git push` sin que el usuario lo pida.
