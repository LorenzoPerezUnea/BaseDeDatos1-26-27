# Orden lógico de ejecución

## Introducción

Cuando escribimos una consulta SQL seguimos un orden determinado.

Por ejemplo:

```sql
SELECT
    Nombre,
    Precio
FROM Producto
WHERE Precio > 100
ORDER BY Precio;
```

Da la impresión de que MySQL ejecuta la consulta exactamente en ese mismo orden.

Sin embargo, internamente ocurre algo muy diferente.

Aunque nosotros escribimos primero `SELECT`, el servidor ​**no comienza seleccionando las columnas**​.

Comprender el orden lógico de ejecución es fundamental para entender por qué algunas consultas producen errores y cómo optimizarlas.

---

## El orden en que escribimos la consulta

El orden sintáctico que utilizamos normalmente es:

```text
SELECT

FROM

WHERE

ORDER BY

LIMIT
```

Este orden está pensado para facilitar la escritura y la lectura por parte de las personas.

No representa el funcionamiento interno del motor de la base de datos.

---

## El orden lógico de ejecución

Internamente MySQL procesa la consulta siguiendo un orden muy diferente.

```text
1. FROM

↓

2. WHERE

↓

3. SELECT

↓

4. ORDER BY

↓

5. LIMIT
```

Cada etapa utiliza el resultado producido por la anterior.

---

## Paso 1. FROM

Lo primero que hace MySQL es localizar la tabla indicada.

```sql
FROM Producto
```

En este momento todavía no se han seleccionado columnas ni se ha filtrado ningún registro.

Simplemente se obtiene el conjunto inicial de datos.

---

## Paso 2. WHERE

A continuación se aplican los filtros.

```sql
WHERE Precio > 100
```

Todas las filas que no cumplen la condición son descartadas.

A partir de este punto únicamente continúan las filas válidas.

---

## Paso 3. SELECT

Solo ahora se seleccionan las columnas solicitadas.

```sql
SELECT
    Nombre,
    Precio
```

Las demás columnas dejan de formar parte del resultado.

---

## Paso 4. ORDER BY

Una vez obtenido el conjunto definitivo de filas y columnas, MySQL las ordena.

```sql
ORDER BY Precio DESC
```

El contenido no cambia.

Únicamente cambia el orden de presentación.

---

## Paso 5. LIMIT

Finalmente se limita el número de filas.

```sql
LIMIT 10
```

Si el resultado contiene cien registros, únicamente se mostrarán los diez primeros.

---

## Ejemplo completo

Consideremos la siguiente consulta.

```sql
SELECT
    Nombre,
    Precio
FROM Producto
WHERE Activo = TRUE
ORDER BY Precio DESC
LIMIT 3;
```

MySQL realiza internamente las siguientes operaciones:

1. Carga la tabla `Producto`.
2. Conserva únicamente los productos activos.
3. Selecciona las columnas `Nombre` y `Precio`.
4. Ordena los resultados por precio descendente.
5. Devuelve únicamente los tres primeros registros.

Comprender este flujo facilita enormemente el diseño de consultas más complejas.

---

## ¿Por qué es importante?

Muchas dudas habituales desaparecen al comprender este orden lógico.

Por ejemplo:

* ¿Por qué no puedo utilizar un alias creado en `SELECT` dentro de `WHERE`?
* ¿Por qué `LIMIT` actúa después de ordenar?
* ¿Por qué `ORDER BY` puede utilizar columnas que no aparecen en el resultado?

Todas estas preguntas se responden observando el orden interno de ejecución.

Más adelante, cuando estudiemos `GROUP BY` y `HAVING`, veremos que este orden lógico será todavía más importante.

---

## Ideas clave

* El orden en que escribimos una consulta no coincide con el orden en que MySQL la ejecuta.
* `FROM` es el primer paso lógico.
* `WHERE` filtra los registros antes de seleccionar las columnas.
* `ORDER BY` organiza el resultado obtenido.
* `LIMIT` actúa siempre al final del proceso.
* Comprender este flujo facilita la escritura y depuración de consultas SQL.

