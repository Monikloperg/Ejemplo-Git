# Requerimientos: Ejemplo (calculadora de descuentos)

> Plantilla de ejemplo. Copia la carpeta `specs/ejemplo/` y renómbrala con el nombre de tu funcionalidad.

## Introducción

Breve descripción de la funcionalidad y del problema que resuelve (el "para qué").

## Requisitos

### Requisito 1: Calcular descuento por porcentaje

**Historia de usuario:** Como vendedor, quiero aplicar un porcentaje de descuento a un precio, para mostrar al cliente el valor final.

**Criterios de aceptación**

- 1.1 Dado un precio y un porcentaje entre 0 y 100, el sistema devuelve el precio final con el descuento aplicado.
- 1.2 Si el porcentaje es menor que 0 o mayor que 100, el sistema rechaza la operación con un mensaje de error claro.
- 1.3 El resultado se redondea a 2 decimales.

### Requisito 2: Descuento máximo permitido

**Historia de usuario:** Como administrador, quiero limitar el descuento máximo, para proteger el margen del negocio.

**Criterios de aceptación**

- 2.1 El sistema no permite descuentos superiores al máximo configurado (por defecto 50 %).
- 2.2 Al exceder el máximo, el sistema informa cuál es el límite vigente.

## Fuera de alcance

- Descuentos acumulables y cupones.
