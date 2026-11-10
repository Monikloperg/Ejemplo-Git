# Tareas: Registrar gastos (MIS FINANZAS)

> Marca `[x]` solo cuando `task-verificator` haya emitido el veredicto CUMPLE para la tarea.

- [ ] 1. Preparar la estructura del proyecto
  - Crear `src/mis_finanzas/__init__.py`, `tests/` y la configuración de `pytest` (`pytest.ini` con `pythonpath = src`).
  - Verificar que `python -m pytest` se ejecuta sin errores de importación.
  - _Requisitos: ninguno (preparación)_

- [ ] 2. Implementar el modelo y las validaciones
  - [ ] 2.1 Crear `Gasto`, `CATEGORIAS`, `ErrorValidacion` y `validar_gasto` en `modelos.py`.
    - _Requisitos: 2.1, 2.2, 2.3_
  - [ ] 2.2 Escribir `tests/test_modelos.py` con los casos válidos, los límites y cada mensaje de error.
    - _Requisitos: 2.1, 2.2, 2.3_

- [ ] 3. Implementar la persistencia en JSON
  - [ ] 3.1 Crear `RepositorioJSON` y `ErrorAlmacenamiento` en `repositorio.py` (cargar, guardar, ruta configurable, archivo inexistente y JSON corrupto).
    - _Requisitos: 3.1, 3.2, 3.3_
  - [ ] 3.2 Escribir `tests/test_repositorio.py` (ida y vuelta, archivo inexistente, JSON corrupto sin modificar el archivo).
    - _Requisitos: 3.1, 3.2, 3.3_

- [ ] 4. Implementar el registro de gastos
  - [ ] 4.1 Crear `ServicioGastos.registrar_gasto` en `servicio.py`: validar, asignar `id` único, usar la fecha de hoy por defecto y persistir; un gasto inválido no toca el archivo.
    - _Requisitos: 1.1, 1.2, 1.3, 2.4_
  - [ ] 4.2 Escribir las pruebas de registro en `tests/test_servicio.py` (incluida la persistencia entre dos instancias).
    - _Requisitos: 1.1, 1.2, 1.3, 2.4_

- [ ] 5. Implementar la consulta de gastos
  - [ ] 5.1 Agregar `listar_gastos` (más reciente primero) y `total` a `ServicioGastos`.
    - _Requisitos: 4.1, 4.2, 4.3_
  - [ ] 5.2 Escribir las pruebas de listado y total (orden, varios gastos y caso vacío).
    - _Requisitos: 4.1, 4.2, 4.3_
