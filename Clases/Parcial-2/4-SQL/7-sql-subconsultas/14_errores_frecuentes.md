# Errores frecuentes

## Introducción

Las subconsultas son uno de los temas que más dificultades suelen presentar durante el aprendizaje de SQL.

La mayoría de los errores no se deben a la sintaxis, sino a no comprender **qué devuelve realmente una subconsulta** y ​**cuándo se ejecuta**​.

Conocer los errores más habituales permitirá detectarlos rápidamente y escribir consultas mucho más robustas.

---

# Error 1. La subconsulta devuelve más de una fila

Es el error más frecuente.

Supongamos la siguiente consulta:

```sql
SELECT
    Nombre
FROM Producto
WHERE Precio =
(
    SELECT Precio
    FROM Producto
    WHERE IdCategoria = 3
);
```

Si la categoría contiene varios productos, la subconsulta devuelve varios precios.

MySQL mostrará un mensaje similar a:

```text
ERROR 1242 (21000)

Subquery returns more than 1 row
```

## Solución

Si esperamos varios valores debemos utilizar operadores como:

* `IN`
* `ANY`
* `ALL`
* `EXISTS`

Por ejemplo:

```sql
SELECT
    Nombre
FROM Producto
WHERE Precio IN
(
    SELECT Precio
    FROM Producto
    WHERE IdCategoria = 3
);
```

---

# Error 2. Olvidar el alias en una subconsulta de FROM

Incorrecto:

```sql
SELECT *
FROM
(
    SELECT
        IdCliente,
        SUM(Total)
    FROM Pedido
    GROUP BY IdCliente
);
```

MySQL mostrará un error porque la tabla derivada no tiene nombre.

## Correcto

```sql
SELECT *
FROM
(
    SELECT
        IdCliente,
        SUM(Total) AS TotalVentas
    FROM Pedido
    GROUP BY IdCliente
) AS Ventas;
```

Toda subconsulta situada en `FROM` debe tener un alias.

---

# Error 3. Confundir JOIN con subconsulta

Muchos estudiantes intentan resolver todos los problemas utilizando únicamente `JOIN`.

Otros utilizan subconsultas para todo.

Ninguna de las dos estrategias es correcta.

Debemos elegir la herramienta adecuada según el problema:

* combinar información → `JOIN`;
* calcular valores → subconsultas;
* comprobar existencia → `EXISTS`.

---

# Error 4. No entender las subconsultas correlacionadas

Observa:

```sql
SELECT
    c.Nombre,
    (
        SELECT COUNT(*)
        FROM Pedido p
        WHERE p.IdCliente = c.IdCliente
    )
FROM Cliente c;
```

Muchos estudiantes creen que la subconsulta se ejecuta una única vez.

No es así.

Se ejecuta una vez para cada cliente.

Comprender este detalle resulta esencial para entender el rendimiento de la consulta.

---

# Error 5. Utilizar COUNT() para comprobar existencia

Incorrecto:

```sql
SELECT
    Nombre
FROM Cliente c
WHERE
(
    SELECT COUNT(*)
    FROM Pedido p
    WHERE p.IdCliente = c.IdCliente
) > 0;
```

Correcto:

```sql
SELECT
    Nombre
FROM Cliente c
WHERE EXISTS
(
    SELECT 1
    FROM Pedido p
    WHERE p.IdCliente = c.IdCliente
);
```

La segunda consulta expresa mucho mejor la intención.

---

# Error 6. Escribir consultas innecesariamente complejas

A veces encontramos consultas con varios niveles de subconsultas cuando bastaría una sola.

Ejemplo poco recomendable:

```text
Consulta

↓

Subconsulta

↓

Subconsulta

↓

Subconsulta
```

Siempre que sea posible debemos buscar la solución más sencilla.

---

# Error 7. Utilizar SELECT \*

Dentro de las subconsultas también debemos seleccionar únicamente las columnas necesarias.

Incorrecto:

```sql
SELECT *
```

Mejor:

```sql
SELECT Precio
```

o

```sql
SELECT SUM(Total)
```

Cuantas menos columnas procese MySQL, más eficiente será la consulta.

---

# Error 8. No probar la subconsulta por separado

Una excelente práctica consiste en ejecutar primero la subconsulta de forma independiente.

Por ejemplo:

```sql
SELECT AVG(Precio)
FROM Producto;
```

Una vez comprobado el resultado, podemos integrarla dentro de la consulta principal.

Este método facilita enormemente la detección de errores.

---

# Error 9. No utilizar alias descriptivos

Incorrecto:

```sql
SELECT *
FROM
(
    ...
) AS t;
```

Mejor:

```sql
SELECT *
FROM
(
    ...
) AS VentasClientes;
```

Los alias descriptivos hacen que el código sea mucho más fácil de leer y mantener.

---

# Recomendaciones

Antes de ejecutar una subconsulta conviene comprobar:

* ¿Devuelve un valor o varios?
* ¿Necesita un alias?
* ¿Puede sustituirse por `EXISTS`?
* ¿Es realmente necesaria?
* ¿Está utilizando únicamente las columnas necesarias?

Responder a estas preguntas evita la mayoría de los errores.

---

## Ideas clave

* El error "Subquery returns more than 1 row" suele indicar que estamos utilizando un operador inadecuado.
* Las subconsultas de `FROM` siempre necesitan un alias.
* Las subconsultas correlacionadas se ejecutan una vez por cada fila de la consulta principal.
* `EXISTS` suele ser preferible a `COUNT()` para comprobar la existencia de registros.
* Probar primero la subconsulta de forma independiente facilita enormemente la depuración.

