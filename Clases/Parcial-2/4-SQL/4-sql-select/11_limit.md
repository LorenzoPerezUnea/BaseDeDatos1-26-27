# LIMIT

## Introducción

En bases de datos pequeñas resulta habitual visualizar todos los registros devueltos por una consulta.

Sin embargo, en entornos reales una tabla puede contener millones de filas.

Mostrar toda esa información no solo sería lento, sino también inútil para el usuario.

Con frecuencia únicamente necesitamos visualizar:

* los primeros 10 productos;
* los últimos 20 pedidos;
* los 5 empleados más recientes;
* los 100 clientes con mayor actividad.

Para resolver esta necesidad SQL incorpora la cláusula `LIMIT`.

---

## ¿Qué hace LIMIT?

`LIMIT` restringe el número máximo de filas devueltas por una consulta.

Su sintaxis básica es:

```sql
SELECT columnas
FROM Tabla
LIMIT cantidad;
```

La consulta seguirá procesándose normalmente, pero únicamente se mostrarán las primeras filas solicitadas.

---

## Primer ejemplo

Mostrar únicamente los tres primeros productos.

```sql
SELECT *
FROM Producto
LIMIT 3;
```

Resultado:

| Id | Nombre    | Precio |
| ---: | ----------- | -------: |
|  1 | Portátil | 950.00 |
|  2 | Monitor   | 280.00 |
|  3 | Ratón    |  25.00 |

Aunque la tabla contenga cientos de productos, solo aparecerán tres.

---

## LIMIT y ORDER BY

Normalmente `LIMIT` se utiliza junto con `ORDER BY`.

Por ejemplo, obtener los cinco productos más caros.

```sql
SELECT
    Nombre,
    Precio
FROM Producto
ORDER BY Precio DESC
LIMIT 5;
```

Primero MySQL ordena todos los productos por precio y después devuelve únicamente los cinco primeros.

Este patrón aparece constantemente en aplicaciones empresariales.

---

## Paginación de resultados

También es posible indicar desde qué fila comenzar.

```sql
SELECT *
FROM Producto
LIMIT 10, 5;
```

En este caso:

* se omiten las diez primeras filas;
* se muestran las cinco siguientes.

Esta técnica constituye la base de la paginación utilizada en la mayoría de aplicaciones web.

Más adelante estudiaremos alternativas más eficientes para conjuntos de datos muy grandes.

---

## Casos de uso habituales

`LIMIT` aparece en multitud de situaciones:

* mostrar los últimos pedidos;
* visualizar los productos más vendidos;
* obtener una muestra de datos;
* comprobar rápidamente el contenido de una tabla;
* limitar resultados durante el desarrollo de consultas.

---

## Buenas prácticas

Durante el desarrollo resulta muy recomendable utilizar `LIMIT`.

Si una tabla contiene millones de registros, trabajar con un pequeño subconjunto facilita enormemente las pruebas y reduce el tiempo de ejecución de las consultas.

Una vez validada la consulta, `LIMIT` puede eliminarse si se desea obtener el conjunto completo de resultados.

---

## Errores frecuentes

Entre los errores más comunes encontramos:

* utilizar `LIMIT` sin ordenar previamente los datos cuando se espera un resultado concreto;
* creer que `LIMIT` modifica la tabla;
* pensar que siempre devuelve "los primeros registros insertados".

Sin `ORDER BY`, el concepto de "primeros registros" no está garantizado.

---

## Ideas clave

* `LIMIT` restringe el número de filas devueltas por una consulta.
* Es especialmente útil sobre tablas de gran tamaño.
* Habitualmente se combina con `ORDER BY`.
* Permite implementar paginación de resultados.
* Constituye una herramienta muy utilizada durante el desarrollo y la depuración de consultas.

