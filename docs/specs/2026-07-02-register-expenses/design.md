# Diseño: Registrar gastos (MIS FINANZAS)

## Visión general

Un paquete Python `mis_finanzas` en capas simples y sin dependencias externas (solo biblioteca estándar; `pytest` para pruebas):

```
src/mis_finanzas/
├── __init__.py
├── modelos.py        # Gasto, CATEGORIAS, validación
├── repositorio.py    # RepositorioJSON: leer/guardar el archivo
└── servicio.py       # ServicioGastos: registrar, listar, total
tests/
├── test_modelos.py
├── test_repositorio.py
└── test_servicio.py
```

Flujo de `registrar_gasto`: el servicio valida los datos (modelo) → asigna `id` → el repositorio carga la lista, agrega el gasto y guarda el archivo.

## Componentes e interfaces

### `modelos.py`

- `CATEGORIAS = ("alimentacion", "transporte", "servicios", "salud", "entretenimiento", "otros")`
- `class ErrorValidacion(ValueError)`: error de datos inválidos.
- `@dataclass(frozen=True) class Gasto`: campos `id: str`, `monto: float`, `fecha: date`, `categoria: str`.
- `validar_gasto(monto, fecha, categoria, hoy=None) -> None`: lanza `ErrorValidacion` según la tabla de errores. El parámetro `hoy` permite probar sin depender del reloj.

### `repositorio.py`

- `class ErrorAlmacenamiento(Exception)`: archivo ilegible o con JSON inválido.
- `class RepositorioJSON(ruta)`:
  - `cargar() -> list[Gasto]`: devuelve `[]` si el archivo no existe.
  - `guardar(gastos: list[Gasto]) -> None`: escribe el JSON completo (crea carpetas si faltan).

### `servicio.py`

- `class ServicioGastos(repositorio, hoy=None)`:
  - `registrar_gasto(monto, categoria, fecha=None) -> Gasto`
  - `listar_gastos() -> list[Gasto]` (más reciente primero)
  - `total() -> float`

## Modelo de datos

Archivo JSON: una lista de objetos. La fecha se guarda en formato ISO `AAAA-MM-DD`.

```json
[
  {"id": "7c1f...", "monto": 25000.0, "fecha": "2026-07-01", "categoria": "alimentacion"}
]
```

El `id` se genera con `uuid.uuid4().hex`.

## Manejo de errores

| Caso | Respuesta | Requisito |
|---|---|---|
| `monto` no numérico o `<= 0` | `ErrorValidacion("El monto debe ser mayor que 0")` | 2.1 |
| `fecha > hoy` | `ErrorValidacion("La fecha no puede ser futura")` | 2.2 |
| `categoria` fuera de `CATEGORIAS` | `ErrorValidacion("Categoría inválida. Permitidas: alimentacion, transporte, ...")` | 2.3 |
| Cualquier error de validación | No se llama a `guardar`; el archivo queda intacto | 2.4 |
| JSON corrupto al cargar | `ErrorAlmacenamiento` con el motivo; el archivo no se modifica | 3.3 |
| Archivo inexistente | Se interpreta como lista vacía; se crea al guardar | 3.2 |

## Estrategia de pruebas

Pruebas unitarias con `pytest`, usando `tmp_path` para los archivos y `hoy` inyectado para las fechas.

- **Modelo:** monto 0, negativo, texto; fecha de hoy (válida) y de mañana (inválida); categoría válida e inválida.
- **Repositorio:** archivo inexistente → `[]`; guardar y volver a cargar devuelve los mismos gastos; JSON corrupto → `ErrorAlmacenamiento` y archivo sin cambios; ruta configurable.
- **Servicio:** registrar asigna `id` único y fecha de hoy por defecto; un gasto inválido no modifica el archivo; persistencia entre dos instancias del servicio; listado ordenado; total con 0 y con varios gastos.

Comando: `python -m pytest`.
