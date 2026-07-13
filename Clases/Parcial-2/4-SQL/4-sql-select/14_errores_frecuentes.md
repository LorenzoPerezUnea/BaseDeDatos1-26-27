# Errores frecuentes

## Introducción

Aprender SQL no consiste únicamente en memorizar la sintaxis.

Una parte muy importante del aprendizaje consiste en interpretar correctamente los errores y comprender por qué una consulta no devuelve el resultado esperado.

Durante las primeras prácticas es completamente normal cometer errores. De hecho, incluso los desarrolladores con experiencia reciben mensajes de error continuamente mientras escriben nuevas consultas.

La diferencia está en saber identificarlos y corregirlos de forma sistemática.

En este apartado recopilamos los errores más habituales relacionados con la sentencia `SELECT`.

---

## Error 1. Olvidar la cláusula FROM

Uno de los errores más frecuentes consiste en escribir:

```sql
SELECT Nombre;
```

MySQL no sabe de qué tabla debe obtener esa columna.

La consulta correcta sería:

```sql
SELECT Nombre
FROM Cliente;
```

Siempre debemos indicar el origen de los datos.

---

## Error 2. Escribir mal el nombre de una columna

Supongamos que la tabla contiene la columna:

```text
CorreoElectronico
```

Si escribimos:

```sql
SELECT Correo
FROM Cliente;
```

MySQL devolverá un error indicando que la columna no existe.

Los nombres utilizados en la consulta deben coincidir exactamente con los definidos en la tabla.

---

## Error 3. Utilizar = con NULL

Muchos estudiantes escriben:

```sql
SELECT *
FROM Cliente
WHERE Telefono = NULL;
```

Esta consulta nunca funcionará correctamente.

La forma correcta es:

```sql
SELECT *
FROM Cliente
WHERE Telefono IS NULL;
```

Recordemos que `NULL` representa la ausencia de un valor y posee operadores específicos.

---

## Error 4. Confundir = con LIKE

Si queremos buscar clientes cuyo nombre empiece por "A", esta consulta es incorrecta:

```sql
SELECT *
FROM Cliente
WHERE Nombre = 'A%';
```

El operador `=` busca coincidencias exactas.

La consulta correcta es:

```sql
SELECT *
FROM Cliente
WHERE Nombre LIKE 'A%';
```

---

## Error 5. Utilizar AND cuando debería utilizarse OR

Supongamos que escribimos:

```sql
SELECT *
FROM Cliente
WHERE
    Ciudad = 'Santander'
    AND Ciudad = 'Bilbao';
```

La consulta no devolverá ningún registro.

Un cliente no puede pertenecer simultáneamente a dos ciudades distintas.

La consulta correcta sería:

```sql
SELECT *
FROM Cliente
WHERE
    Ciudad = 'Santander'
    OR Ciudad = 'Bilbao';
```

---

## Error 6. Olvidar ORDER BY antes de LIMIT

Muchos estudiantes escriben:

```sql
SELECT *
FROM Producto
LIMIT 5;
```

Pensando que obtendrán los cinco productos más caros.

En realidad, únicamente obtendrán cinco registros cualquiera.

La consulta correcta sería:

```sql
SELECT *
FROM Producto
ORDER BY Precio DESC
LIMIT 5;
```

Siempre que queramos los "primeros", "últimos", "más caros" o "más recientes", debemos ordenar previamente.

---

## Error 7. Abusar de SELECT \*

Aunque durante el aprendizaje utilizaremos con frecuencia:

```sql
SELECT *
FROM Cliente;
```

En aplicaciones profesionales normalmente resulta preferible escribir:

```sql
SELECT
    Nombre,
    Ciudad
FROM Cliente;
```

Seleccionar únicamente las columnas necesarias mejora la claridad de la consulta y reduce la cantidad de datos transferidos.

---

## Error 8. No utilizar alias descriptivos

Una consulta como:

```sql
SELECT
    Nombre AS X,
    Ciudad AS Y
FROM Cliente;
```

funciona correctamente, pero resulta muy difícil de interpretar.

Es preferible utilizar nombres significativos.

```sql
SELECT
    Nombre AS Cliente,
    Ciudad AS CiudadResidencia
FROM Cliente;
```

El código será mucho más fácil de mantener.

---

## Recomendaciones para depurar consultas

Cuando una consulta no funcione, conviene seguir siempre el mismo procedimiento:

1. Leer cuidadosamente el mensaje de error.
2. Comprobar la sintaxis.
3. Verificar los nombres de tablas y columnas.
4. Revisar las condiciones del `WHERE`.
5. Ejecutar consultas más sencillas para aislar el problema.
6. Añadir complejidad progresivamente.

Esta metodología permite localizar la mayoría de los errores en muy poco tiempo.

---

## Ideas clave

* La mayoría de los errores se deben a pequeños descuidos de sintaxis.
* `FROM` y `WHERE` son el origen de muchos errores durante las primeras prácticas.
* `NULL` requiere operadores específicos (`IS NULL` e `IS NOT NULL`).
* `ORDER BY` y `LIMIT` suelen utilizarse conjuntamente.
* Aprender a interpretar los mensajes de error forma parte del trabajo habitual con SQL.

