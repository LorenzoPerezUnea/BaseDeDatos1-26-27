# Buenas prácticas al usar JOIN

## Introducción

A medida que las consultas crecen, los errores también aumentan.

Una consulta con cinco o seis tablas puede seguir siendo fácil de entender... o convertirse en un código prácticamente imposible de mantener.

Por ello es importante adoptar una serie de buenas prácticas desde el principio.

---

## 1. Utilizar siempre alias

En lugar de escribir continuamente:

```sql
Cliente.Nombre
```

es preferible utilizar:

```sql
c.Nombre
```

Definiendo previamente:

```sql
FROM Cliente AS c
```

Los alias reducen el tamaño de la consulta y mejoran notablemente su legibilidad.

---

## 2. Escribir cada JOIN en una línea independiente

Evita escribir consultas compactas.

En lugar de:

```sql
FROM Cliente c INNER JOIN Pedido p ON c.IdCliente=p.IdCliente INNER JOIN Producto pr ON ...
```

es preferible:

```sql
FROM Cliente AS c

INNER JOIN Pedido AS p
ON c.IdCliente = p.IdCliente

INNER JOIN Producto AS pr
ON ...
```

Esta estructura permite localizar errores mucho más rápidamente.

---

## 3. Seleccionar únicamente las columnas necesarias

Evita utilizar:

```sql
SELECT *
```

Cuando intervienen muchas tablas, esta práctica puede devolver decenas o cientos de columnas innecesarias.

Es mejor seleccionar únicamente las que realmente serán utilizadas.

---

## 4. Utilizar nombres descriptivos

Cuando dos tablas poseen columnas con el mismo nombre, conviene utilizar alias en el resultado.

```sql
SELECT
    c.Nombre AS Cliente,
    e.Nombre AS Empleado
```

Esto evita ambigüedades tanto para el usuario como para la aplicación.

---

## 5. Revisar cuidadosamente la condición ON

Uno de los errores más graves consiste en unir columnas incorrectas.

Por ejemplo:

```sql
ON Cliente.IdCliente = Producto.IdProducto
```

La consulta puede ejecutarse sin producir errores, pero el resultado será completamente incorrecto.

Antes de ejecutar una consulta conviene comprobar siempre que las columnas relacionadas pertenecen realmente a la misma relación.

---

## 6. Utilizar el tipo de JOIN adecuado

Antes de escribir una consulta conviene responder una pregunta muy sencilla:

> ¿Quiero únicamente las coincidencias o quiero conservar una de las tablas completa?

La respuesta determina el tipo de JOIN:

* solo coincidencias → `INNER JOIN`;
* conservar la izquierda → `LEFT JOIN`;
* conservar la derecha → `RIGHT JOIN`.

---

## 7. Mantener un orden lógico

Es recomendable seguir el mismo recorrido que muestra el modelo entidad-relación.

Por ejemplo:

```text
Cliente

↓

Pedido

↓

Detalle

↓

Producto

↓

Categoría
```

De esta manera cualquier desarrollador puede comprender la consulta rápidamente.

---

## 8. Comprobar los resultados

Antes de dar una consulta por válida:

* revisa el número de filas;
* comprueba algunos registros manualmente;
* verifica que no existan duplicados inesperados;
* compara los resultados con los datos almacenados.

Una consulta sintácticamente correcta no siempre produce resultados correctos.

---

## Ideas clave

* Utiliza alias de forma consistente.
* Escribe un `JOIN` por línea para mejorar la legibilidad.
* Evita `SELECT *` en consultas complejas.
* Comprueba cuidadosamente la condición de cada `ON`.
* Elige el tipo de `JOIN` adecuado según el resultado esperado.
* Mantén una estructura clara y coherente para facilitar el mantenimiento del código.

