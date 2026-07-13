# Funciones de agregación

## Introducción

Las funciones de agregación permiten realizar cálculos sobre un conjunto de filas y devolver ​**un único valor como resultado**​.

En lugar de procesar cada registro de forma independiente, SQL considera el conjunto completo (o cada grupo creado mediante `GROUP BY`) y calcula un resumen.

Este tipo de funciones constituye la base de:

* informes empresariales;
* cuadros de mando (​*dashboards*​);
* análisis estadísticos;
* inteligencia de negocio (Business Intelligence);
* minería de datos.

Prácticamente cualquier informe que muestre totales, medias o máximos utiliza funciones de agregación.

---

## ¿Cómo funcionan?

Supongamos la siguiente tabla `Producto`.

| Id | Nombre    | Precio |
| ---: | ----------- | -------: |
|  1 | Ratón    |     25 |
|  2 | Monitor   |    280 |
|  3 | SSD       |    120 |
|  4 | Portátil |    950 |

Una consulta tradicional devuelve las cuatro filas.

```sql
SELECT
    Nombre,
    Precio
FROM Producto;
```

En cambio, una función de agregación resume toda la tabla.

```sql
SELECT
    AVG(Precio)
FROM Producto;
```

Resultado:

| AVG(Precio) |
| ------------: |
|      343.75 |

Cuatro registros han producido un único resultado.

---

## Las cinco funciones principales

Durante esta asignatura trabajaremos principalmente con cinco funciones de agregación.

| Función      | Descripción             |
| --------------- | -------------------------- |
| `COUNT()` | Cuenta registros         |
| `SUM()`   | Suma valores             |
| `AVG()`   | Calcula la media         |
| `MIN()`   | Obtiene el valor mínimo |
| `MAX()`   | Obtiene el valor máximo |

Estas funciones están disponibles en prácticamente todos los sistemas gestores de bases de datos relacionales.

---

## Agregación sobre toda la tabla

Si no utilizamos `GROUP BY`, la función se aplica a ​**todos los registros seleccionados**​.

```sql
SELECT
    SUM(Precio)
FROM Producto;
```

La consulta calcula el precio total de todos los productos existentes en la tabla.

En este caso únicamente se obtiene una fila como resultado.

---

## Agregación tras aplicar WHERE

Las funciones de agregación respetan los filtros establecidos mediante `WHERE`.

```sql
SELECT
    AVG(Precio)
FROM Producto
WHERE Activo = TRUE;
```

Primero se seleccionan únicamente los productos activos y, posteriormente, se calcula la media.

Esto vuelve a demostrar el orden lógico de ejecución que estudiamos en la clase anterior.

---

## Agregación y NULL

Un aspecto importante es el tratamiento de los valores `NULL`.

En general:

* `SUM()`, `AVG()`, `MIN()` y `MAX()`​**ignoran los valores NULL**​.
* `COUNT(columna)` únicamente cuenta las filas cuyo valor no sea `NULL`.
* `COUNT(*)` cuenta todas las filas, independientemente de su contenido.

Comprender esta diferencia evitará numerosos errores durante el desarrollo de consultas.

---

## Alias en funciones

Las funciones suelen devolver nombres de columna poco descriptivos.

Por ejemplo:

```sql
SELECT
    AVG(Precio)
FROM Producto;
```

produce un encabezado similar a:

```text
AVG(Precio)
```

Es preferible utilizar un alias.

```sql
SELECT
    AVG(Precio) AS PrecioMedio
FROM Producto;
```

Resultado:

| PrecioMedio |
| ------------: |
|      343.75 |

Los alias mejoran considerablemente la legibilidad de informes y aplicaciones.

---

## Buenas prácticas

Cuando utilices funciones de agregación recuerda siempre:

* asignar alias descriptivos;
* filtrar previamente los datos con `WHERE` cuando sea necesario;
* comprobar el efecto de los valores `NULL`;
* utilizar el tipo de función adecuado para cada problema.

---

## Ideas clave

* Las funciones de agregación resumen múltiples filas en un único resultado.
* Las cinco funciones principales son `COUNT`, `SUM`, `AVG`, `MIN` y `MAX`.
* Si no existe `GROUP BY`, la agregación se realiza sobre toda la tabla.
* `WHERE` filtra los datos antes de ejecutar la función.
* Es recomendable utilizar alias para nombrar el resultado de la agregación.

