# Tareas: Ejemplo (calculadora de descuentos)

> Plantilla de ejemplo. Cada tarea cita los requisitos que cubre; `task-verificator` usa esas referencias.
> Marca `[x]` solo cuando la tarea haya sido verificada.

- [ ] 1. Crear la estructura del módulo
  - Crear `src/descuentos.py` y `tests/test_descuentos.py`.
  - _Requisitos: ninguno (preparación)_

- [ ] 2. Implementar el cálculo del descuento
  - [ ] 2.1 Implementar `calcular_descuento(precio, porcentaje)` con redondeo a 2 decimales.
    - _Requisitos: 1.1, 1.3_
  - [ ] 2.2 Escribir pruebas del caso válido y del redondeo.
    - _Requisitos: 1.1, 1.3_

- [ ] 3. Validar las entradas
  - [ ] 3.1 Rechazar porcentajes fuera de 0–100 y precios negativos con `ValueError`.
    - _Requisitos: 1.2_
  - [ ] 3.2 Escribir pruebas de los límites y de cada error.
    - _Requisitos: 1.2_

- [ ] 4. Aplicar el descuento máximo
  - [ ] 4.1 Rechazar descuentos mayores al máximo (50 % por defecto) indicando el límite.
    - _Requisitos: 2.1, 2.2_
  - [ ] 4.2 Escribir pruebas del máximo y del mensaje de error.
    - _Requisitos: 2.1, 2.2_
