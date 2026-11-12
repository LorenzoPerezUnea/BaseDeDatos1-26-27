# ORDER BY

## Introducción

Hasta ahora las consultas realizadas se han centrado principalmente en decidir **qué registros aparecen** en el resultado.

Sin embargo, en muchas situaciones también necesitamos controlar ​**el orden en el que se muestran esos registros**​.

Por ejemplo:

* mostrar los clientes ordenados alfabéticamente por nombre;
* mostrar los productos de mayor a menor precio;
* mostrar los pedidos más recientes primero;
* ordenar los empleados por departamento y, dentro de cada departamento, por salario.

Para realizar estas operaciones SQL proporciona la cláusula `<strong>ORDER BY</strong>`.

---

## ¿Qué hace ORDER BY?

`ORDER BY` permite indicar el criterio utilizado para ordenar las filas devueltas por una consulta.

Por ejemplo:

```
SELECT *
FROM Cliente
ORDER BY Nombre;
```

La consulta devuelve todos los clientes ordenados por el valor de la columna `Nombre`.

Por defecto, SQL utiliza un orden ​**ascendente**​.

Por tanto:

```
ORDER BY Nombre;
```

equivale a:

```
ORDER BY Nombre ASC;
```

---

## Orden ascendente y descendente

Podemos indicar explícitamente el sentido de la ordenación mediante:

* `ASC` → orden ascendente;
* `DESC` → orden descendente.

Por ejemplo:

```
SELECT *
FROM Producto
ORDER BY Precio ASC;
```

muestra los productos desde el precio más bajo hasta el más alto.

En cambio:

```
SELECT *
FROM Producto
ORDER BY Precio DESC;
```

muestra los productos desde el precio más alto hasta el más bajo.

`ASC` es el comportamiento predeterminado, por lo que normalmente puede omitirse.

---

## Ordenar por varias columnas

`ORDER BY` permite utilizar más de una columna.

Por ejemplo:

```
SELECT *
FROM Empleado
ORDER BY Departamento, Apellidos;
```

En este caso SQL aplica los criterios de izquierda a derecha:

1. primero ordena los empleados por `Departamento`;
2. dentro de cada departamento, los ordena por `Apellidos`.

También podemos especificar un sentido diferente para cada columna:

```
SELECT *
FROM Empleado
ORDER BY Departamento ASC, Salario DESC;
```

Primero se ordenan los empleados por departamento de forma ascendente y, dentro de cada departamento, por salario de mayor a menor.

---

## ORDER BY con WHERE

`ORDER BY` puede utilizarse junto con `WHERE`.

La cláusula `WHERE` determina ​**qué registros se muestran**​, mientras que `ORDER BY` determina ​**en qué orden aparecen**​.

Por ejemplo:

```
SELECT *
FROM Producto
WHERE Precio > 100
ORDER BY Precio DESC;
```

La consulta:

1. selecciona los productos cuyo precio es superior a 100;
2. ordena los resultados de mayor a menor precio.

El resultado podría ser:

| Producto  | Precio  |
| ----------- | --------- |
| Portátil | 1450.00 |
| Monitor   | 420.00  |
| Teclado   | 150.00  |

Por tanto, `WHERE` y `ORDER BY` cumplen funciones diferentes y complementarias.

---

## ORDER BY con alias

También podemos ordenar utilizando un alias definido en la cláusula `SELECT`.

Por ejemplo:

```
SELECT
    Nombre,
    Precio,
    Precio * 1.21 AS PrecioConIVA
FROM Producto
ORDER BY PrecioConIVA DESC;
```

En este caso `PrecioConIVA` no es una columna almacenada en la tabla.

Es un ​**alias creado durante la consulta**​, que puede utilizarse para ordenar el resultado.

---

## ORDER BY con expresiones

La columna utilizada para ordenar no tiene que aparecer necesariamente como una columna almacenada en la tabla.

También podemos utilizar expresiones.

Por ejemplo:

```
SELECT
    Nombre,
    Precio
FROM Producto
ORDER BY Precio * 1.21 DESC;
```

SQL calcula la expresión para cada fila y utiliza ese resultado como criterio de ordenación.

Esto resulta especialmente útil cuando queremos ordenar utilizando valores calculados.

---

## ORDER BY y NULL

Cuando una columna contiene valores `NULL`, el comportamiento de su ordenación depende del sistema gestor de bases de datos.

Por ejemplo:

```
SELECT *
FROM Cliente
ORDER BY Telefono;
```

Si algunos clientes tienen `Telefono` con valor `NULL`, su posición dentro del resultado dependerá del gestor y del sentido de ordenación utilizado.

Por ello, cuando el tratamiento de los valores nulos sea importante, conviene consultar el comportamiento específico del SGBD utilizado.

---

## ORDER BY no modifica los datos

Es importante distinguir entre **ordenar el resultado de una consulta** y ​**modificar el orden de los datos almacenados**​.

La siguiente consulta:

```
SELECT *
FROM Cliente
ORDER BY Nombre;
```

no modifica la tabla `Cliente`.

Únicamente establece el orden de las filas en ese resultado concreto.

Si posteriormente se ejecuta:

```
SELECT *
FROM Cliente;
```

no debe suponerse que los clientes aparecerán en el mismo orden.

Una tabla relacional no debe considerarse almacenada en un orden determinado.

---

## Ordenar por posición

Algunos sistemas gestores permiten utilizar la posición de una columna del `SELECT` dentro de `ORDER BY`.

Por ejemplo:

```
SELECT Nombre, Precio
FROM Producto
ORDER BY 2 DESC;
```

El número `2` hace referencia a la segunda columna seleccionada, `Precio`.

Aunque esta sintaxis puede funcionar, generalmente resulta más clara y mantenible utilizar directamente el nombre de la columna o su alias:

```
SELECT Nombre, Precio
FROM Producto
ORDER BY Precio DESC;
```

Por este motivo, se recomienda utilizar nombres o alias en lugar de posiciones numéricas.

---

## Ordenación y rendimiento

Ordenar resultados puede requerir trabajo adicional por parte del sistema gestor de bases de datos, especialmente cuando se trabaja con grandes cantidades de registros.

Por ejemplo:

```
SELECT *
FROM Pedido
ORDER BY Fecha;
```

puede requerir que el SGBD ordene una gran cantidad de filas.

Los índices pueden ayudar al SGBD a resolver determinadas consultas de ordenación de forma más eficiente, aunque su utilización depende de la consulta y de la estructura de la base de datos.

Por ello, en aplicaciones con grandes volúmenes de datos, `ORDER BY` debe utilizarse teniendo en cuenta el rendimiento.

---

## Errores frecuentes

Los errores más habituales son:

* confundir `ASC` con `DESC`;
* olvidar que `ASC` es el comportamiento predeterminado;
* pensar que `ORDER BY` modifica permanentemente el orden de la tabla;
* utilizar una posición numérica cuando un nombre o alias hace la consulta más clara;
* olvidar que el orden de los `NULL` puede depender del SGBD;
* utilizar `ORDER BY` sin tener en cuenta el coste de ordenar grandes cantidades de datos.

Comprender estas diferencias permite construir consultas más claras y predecibles.

---

## Ideas clave

* `ORDER BY` permite ordenar los resultados de una consulta.
* `ASC` establece un orden ascendente y es el comportamiento predeterminado.
* `DESC` establece un orden descendente.
* Se pueden utilizar varias columnas para establecer criterios de ordenación sucesivos.
* `WHERE` determina qué registros aparecen y `ORDER BY` determina cómo se ordenan.
* También se pueden utilizar alias y expresiones como criterios de ordenación.
* `ORDER BY` no modifica los datos almacenados en la tabla.
* El tratamiento de `NULL` durante la ordenación depende del SGBD.
* La ordenación puede tener impacto en el rendimiento de las consultas.

