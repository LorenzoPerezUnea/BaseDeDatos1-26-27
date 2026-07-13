# Errores frecuentes

## Introducción

Las funciones de agregación y las agrupaciones son algunos de los conceptos que más dudas generan al comenzar a trabajar con SQL.

La mayoría de los errores no se deben a la sintaxis, sino a una comprensión incorrecta del orden lógico de ejecución de una consulta.

En este apartado analizaremos los errores más habituales y aprenderemos cómo evitarlos.

---

## Error 1. Olvidar GROUP BY

Muchos estudiantes escriben:

```sql
SELECT
    IdCategoria,
    COUNT(*)
FROM Producto;
```

La consulta intenta mostrar una columna (`IdCategoria`) junto con una función de agregación, pero no indica cómo deben agruparse los registros.

La forma correcta es:

```sql
SELECT
    IdCategoria,
    COUNT(*) AS TotalProductos
FROM Producto
GROUP BY IdCategoria;
```

Siempre que aparezcan columnas no agregadas junto con funciones de agregación, normalmente será necesario utilizar `GROUP BY`.

---

## Error 2. Utilizar WHERE con funciones de agregación

Otro error muy frecuente consiste en escribir:

```sql
SELECT
    Ciudad,
    COUNT(*)
FROM Cliente
WHERE COUNT(*) > 5
GROUP BY Ciudad;
```

`WHERE` no puede utilizar funciones de agregación.

La versión correcta es:

```sql
SELECT
    Ciudad,
    COUNT(*) AS TotalClientes
FROM Cliente
GROUP BY Ciudad
HAVING COUNT(*) > 5;
```

---

## Error 3. Confundir WHERE y HAVING

Recordemos la diferencia.

```text
WHERE
↓
Filtra filas

GROUP BY

HAVING
↓
Filtra grupos
```

Una regla sencilla consiste en recordar:

* **WHERE → registros**
* **HAVING → grupos**

---

## Error 4. Olvidar los alias

Una consulta como:

```sql
SELECT
    AVG(Precio)
FROM Producto;
```

funciona correctamente, pero produce un encabezado poco descriptivo.

Es preferible escribir:

```sql
SELECT
    AVG(Precio) AS PrecioMedio
FROM Producto;
```

---

## Error 5. No comprender el efecto de NULL

Supongamos la siguiente información.

| Cliente | Teléfono |
| --------- | ----------- |
| Ana     | 612345678 |
| Luis    | NULL      |
| Marta   | 698741236 |

La consulta:

```sql
SELECT
    COUNT(Telefono)
FROM Cliente;
```

devuelve:

```text
2
```

Mientras que:

```sql
SELECT
    COUNT(*)
FROM Cliente;
```

devuelve:

```text
3
```

Comprender esta diferencia es fundamental.

---

## Error 6. Agrupar por demasiadas columnas

Es frecuente escribir:

```sql
GROUP BY
    IdCategoria,
    Nombre,
    Precio
```

Cuando se agrupa por demasiadas columnas, cada grupo contiene muy pocos registros y la agregación pierde utilidad.

Conviene agrupar únicamente por los atributos necesarios para responder a la pregunta planteada.

---

## Error 7. Utilizar funciones innecesarias

Muchos principiantes escriben:

```sql
SELECT
    ROUND(
        COUNT(*),
        2
    )
FROM Cliente;
```

`COUNT()` ya devuelve un número entero, por lo que `ROUND()` no aporta ninguna mejora.

Debemos seleccionar únicamente las funciones realmente necesarias.

---

## Error 8. No leer el mensaje de error

MySQL suele indicar con bastante precisión dónde se encuentra el problema.

Antes de modificar una consulta al azar, conviene:

1. leer el mensaje de error;
2. localizar la línea indicada;
3. revisar la sintaxis;
4. ejecutar la consulta paso a paso.

Este hábito reduce considerablemente el tiempo de depuración.

---

## Buenas prácticas

Cuando desarrolles consultas con agrupaciones:

* utiliza alias descriptivos;
* aplica `WHERE` antes de agrupar;
* utiliza `HAVING` únicamente para filtrar grupos;
* revisa siempre el tratamiento de los valores `NULL`;
* construye las consultas de forma incremental.

---

## Ideas clave

* La mayoría de los errores están relacionados con `GROUP BY` y `HAVING`.
* `COUNT(*)` y `COUNT(columna)` no producen el mismo resultado.
* Los alias mejoran la legibilidad.
* Comprender el orden lógico de ejecución facilita la resolución de errores.
* La depuración sistemática es una habilidad esencial para cualquier desarrollador SQL.

