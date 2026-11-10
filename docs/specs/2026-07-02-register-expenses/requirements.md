# Requerimientos: Registrar gastos (MIS FINANZAS)

## Introducción

**MIS FINANZAS** permite a una persona llevar el control de sus gastos personales. Esta primera funcionalidad cubre el **registro de gastos**: capturar un gasto con su monto, fecha y categoría, validarlo, guardarlo en un archivo local y poder consultarlo.

> **Supuestos por confirmar:** (1) "MIS FINANZAS" es el nombre de la aplicación; (2) un gasto tiene exactamente tres campos: monto, fecha y categoría (la descripción libre queda fuera de alcance).

## Glosario

- **Gasto:** registro con `id`, `monto`, `fecha` y `categoria`.
- **Categorías válidas:** `alimentacion`, `transporte`, `servicios`, `salud`, `entretenimiento`, `otros`.

## Requisitos

### Requisito 1: Registrar un gasto

**Historia de usuario:** Como usuario, quiero registrar un gasto con su monto, fecha y categoría, para llevar el control de en qué se va mi dinero.

**Criterios de aceptación**

- 1.1 Dado un monto, una fecha y una categoría válidos, el sistema crea el gasto, le asigna un `id` único y lo devuelve.
- 1.2 Si no se indica la fecha, el sistema usa la fecha de hoy.
- 1.3 El gasto registrado queda guardado de forma persistente: sigue disponible después de reiniciar la aplicación.

### Requisito 2: Validar los datos del gasto

**Historia de usuario:** Como usuario, quiero que el sistema rechace datos inválidos con mensajes claros, para no guardar información errónea.

**Criterios de aceptación**

- 2.1 El monto debe ser un número mayor que 0; en caso contrario se rechaza con el mensaje `El monto debe ser mayor que 0`.
- 2.2 La fecha no puede ser posterior a hoy; en caso contrario se rechaza con el mensaje `La fecha no puede ser futura`.
- 2.3 La categoría debe ser una de las categorías válidas; en caso contrario se rechaza con un mensaje que lista las categorías permitidas.
- 2.4 Un gasto rechazado no se guarda ni modifica el archivo existente.

### Requisito 3: Persistencia en archivo JSON

**Historia de usuario:** Como usuario, quiero que mis gastos se guarden en un archivo local, para no perderlos al cerrar la aplicación.

**Criterios de aceptación**

- 3.1 Los gastos se almacenan en un archivo JSON cuya ruta es configurable.
- 3.2 Si el archivo no existe, el sistema lo trata como una lista vacía de gastos y lo crea al guardar el primero.
- 3.3 Si el archivo existe pero su contenido no es un JSON válido, el sistema informa el error sin sobrescribir ni borrar el archivo.

### Requisito 4: Consultar los gastos

**Historia de usuario:** Como usuario, quiero ver mis gastos y su total, para saber cuánto he gastado.

**Criterios de aceptación**

- 4.1 El sistema lista todos los gastos ordenados por fecha, del más reciente al más antiguo.
- 4.2 El sistema calcula el total de los gastos registrados.
- 4.3 Con cero gastos, la lista está vacía y el total es 0.

## Fuera de alcance

- Editar o eliminar gastos.
- Descripción libre, adjuntos o recibos.
- Presupuestos, ingresos, reportes por categoría y gráficos.
- Múltiples monedas o usuarios.
