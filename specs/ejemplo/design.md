# Diseño: Ejemplo (calculadora de descuentos)

> Plantilla de ejemplo. Describe CÓMO se cumplen los requisitos de `requirements.md`.

## Visión general

Un módulo `descuentos` con una función pura que calcula el precio final y valida las entradas.

## Componentes e interfaces

### `calcular_descuento(precio, porcentaje, maximo=50) -> float`

- **Entradas:** `precio` (número >= 0), `porcentaje` (número), `maximo` (número, por defecto 50).
- **Salida:** precio final redondeado a 2 decimales.
- **Errores:** lanza `ValueError` con mensaje descriptivo (ver manejo de errores).

## Modelo de datos

No hay persistencia. El valor `maximo` por defecto se define como constante `DESCUENTO_MAXIMO = 50`.

## Manejo de errores

| Caso | Respuesta | Requisito |
|---|---|---|
| `porcentaje < 0` o `> 100` | `ValueError("El porcentaje debe estar entre 0 y 100")` | 1.2 |
| `porcentaje > maximo` | `ValueError("El descuento máximo permitido es {maximo}%")` | 2.1, 2.2 |
| `precio < 0` | `ValueError("El precio no puede ser negativo")` | 1.1 |

## Estrategia de pruebas

- Pruebas unitarias para el caso válido, los límites (0, 100, el máximo) y cada error.
- Verificar el redondeo a 2 decimales (1.3).
- Ubicación: `tests/test_descuentos.py`.
