# Operadores lógicos

## Introducción

En muchas consultas una única condición no es suficiente.

Por ejemplo, podríamos necesitar encontrar:

* productos activos **y** con stock disponible;
* clientes de Santander **o** Bilbao;
* empleados que **no** pertenezcan al departamento de ventas;
* productos cuyo precio sea superior a 500 € **y** cuyo stock sea inferior a 10 unidades.

Para construir este tipo de consultas SQL incorpora los ​**operadores lógicos**​.

Estos operadores permiten combinar varias condiciones en una única expresión y constituyen una de las herramientas más utilizadas durante todo el desarrollo de consultas.

---

## Los tres operadores principales

SQL dispone de tres operadores lógicos fundamentales.

| Operador | Significado                              |
| ---------- | ------------------------------------------ |
| AND      | Todas las condiciones deben cumplirse.   |
| OR       | Basta con que se cumpla una de ellas.    |
| NOT      | Invierte el resultado de una condición. |

Estos operadores pueden combinarse entre sí para construir filtros muy complejos.

---

## Operador AND

`AND` exige que todas las condiciones sean verdaderas.

```sql
SELECT
    Nombre,
    Precio,
    Stock
FROM Producto
WHERE
    Precio > 500
    AND Stock > 0;
```

La consulta devolverá únicamente aquellos productos que cumplan ambas condiciones al mismo tiempo.

Si una de ellas no se cumple, el registro será descartado.

---

## Operador OR

`OR` resulta menos restrictivo.

```sql
SELECT
    Nombre,
    Ciudad
FROM Cliente
WHERE
    Ciudad = 'Santander'
    OR Ciudad = 'Bilbao';
```

En este caso aparecerán los clientes de cualquiera de las dos ciudades.

Basta con que una de las condiciones sea verdadera.

---

## Operador NOT

`NOT` invierte el resultado de una condición.

```sql
SELECT *
FROM Producto
WHERE NOT Activo = TRUE;
```

Equivale a consultar los productos inactivos.

También podríamos escribir:

```sql
SELECT *
FROM Producto
WHERE Activo = FALSE;
```

En este caso ambas consultas producen el mismo resultado.

---

## Combinando operadores

Los operadores pueden combinarse para construir consultas más completas.

```sql
SELECT
    Nombre,
    Precio,
    Stock
FROM Producto
WHERE
    Activo = TRUE
    AND Precio > 500
    AND Stock > 5;
```

La consulta únicamente devolverá productos:

* activos;
* con precio superior a 500 €;
* con más de cinco unidades en stock.

---

## Uso de paréntesis

Cuando una consulta combina `AND` y `OR`, es recomendable utilizar paréntesis para indicar claramente el orden de evaluación.

Por ejemplo:

```sql
SELECT *
FROM Cliente
WHERE
(
    Ciudad = 'Santander'
    OR Ciudad = 'Bilbao'
)
AND Activo = TRUE;
```

Los paréntesis mejoran la legibilidad y evitan interpretaciones incorrectas.

---

## Aplicaciones reales

Los operadores lógicos aparecen constantemente en aplicaciones empresariales.

Algunos ejemplos:

* clientes activos de una ciudad determinada;
* productos disponibles y con descuento;
* empleados de varios departamentos;
* pedidos pendientes o en preparación.

Prácticamente cualquier buscador avanzado termina convirtiéndose en una combinación de operadores lógicos.

---

## Errores frecuentes

Los errores más habituales son:

* confundir `AND` con `OR`;
* olvidar utilizar paréntesis en consultas complejas;
* construir condiciones contradictorias que nunca pueden cumplirse.

Una buena práctica consiste en leer la consulta en lenguaje natural antes de ejecutarla.

---

## Ideas clave

* `AND` exige que todas las condiciones sean verdaderas.
* `OR` requiere únicamente una condición verdadera.
* `NOT` invierte el resultado lógico.
* Los operadores lógicos permiten construir filtros complejos.
* El uso de paréntesis mejora la claridad y evita errores en consultas extensas.

