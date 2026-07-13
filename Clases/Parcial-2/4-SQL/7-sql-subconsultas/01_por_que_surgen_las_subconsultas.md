# ¿Por qué surgen las subconsultas?

## Introducción

Hasta ahora todas nuestras consultas seguían un esquema relativamente sencillo.

Seleccionábamos registros de una o varias tablas utilizando:

* `SELECT`;
* `WHERE`;
* `GROUP BY`;
* `HAVING`;
* `JOIN`.

Sin embargo, existen preguntas que requieren ​**utilizar el resultado de una consulta para construir otra**​.

Es precisamente aquí donde nacen las subconsultas.

---

## Un primer problema

Supongamos la tabla `Producto`.

| Id | Producto  | Precio |
| ---: | ----------- | -------: |
|  1 | Ratón    |     25 |
|  2 | Monitor   |    250 |
|  3 | Portátil |    950 |
|  4 | Teclado   |     60 |

Queremos responder la siguiente pregunta:

> **¿Qué productos tienen un precio superior al precio medio de todos los productos?**

---

## Primera idea

Podríamos hacerlo en dos pasos.

Primero:

```sql
SELECT AVG(Precio)
FROM Producto;
```

Resultado:

```text
321.25
```

Después escribir manualmente otra consulta.

```sql
SELECT *
FROM Producto
WHERE Precio > 321.25;
```

Aunque funciona, presenta varios problemas:

* requiere dos consultas;
* el valor puede cambiar con el tiempo;
* obliga al usuario a copiar el resultado.

No es una buena solución.

---

## La solución

Podemos introducir la primera consulta dentro de la segunda.

```sql
SELECT *
FROM Producto
WHERE Precio >
(
    SELECT AVG(Precio)
    FROM Producto
);
```

Ahora MySQL:

1. calcula primero el precio medio;
2. utiliza automáticamente ese resultado;
3. ejecuta la consulta principal.

Todo ocurre en una única sentencia SQL.

---

## ¿Qué es exactamente una subconsulta?

Una subconsulta es una consulta que aparece ​**dentro de otra consulta**​.

Visualmente:

```text
Consulta principal

↓

WHERE

↓

(Subconsulta)

↓

Resultado
```

La consulta interior produce un resultado que la consulta exterior utiliza posteriormente.

---

## ¿Siempre devuelve un único valor?

No.

Dependiendo del problema, una subconsulta puede devolver:

* un único valor;
* una única fila;
* una única columna con múltiples filas;
* varias columnas y varias filas.

Cada situación requiere operadores distintos, que iremos estudiando durante esta clase.

---

## Ventajas

Las subconsultas permiten:

* dividir problemas complejos en pasos sencillos;
* evitar consultas manuales intermedias;
* escribir código más reutilizable;
* construir consultas dinámicas;
* resolver problemas muy difíciles utilizando únicamente SQL.

---

## Aplicaciones reales

Las subconsultas aparecen constantemente en aplicaciones empresariales.

Por ejemplo:

* productos por encima del precio medio;
* empleados con salario superior al promedio;
* clientes con mayor número de compras;
* alumnos con la nota máxima;
* departamentos con más empleados que la media.

En todos estos casos primero es necesario calcular un valor y después utilizarlo en otra consulta.

---

## Ideas clave

* Las subconsultas permiten utilizar el resultado de una consulta dentro de otra.
* Evitan ejecutar varias consultas manualmente.
* SQL ejecuta primero la subconsulta y posteriormente la consulta principal.
* Constituyen una herramienta fundamental para resolver problemas complejos de forma elegante.

