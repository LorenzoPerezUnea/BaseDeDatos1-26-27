# Errores frecuentes

## Introducción

Los `JOIN` son probablemente el tema que más dificultades presenta a los estudiantes cuando comienzan a trabajar con bases de datos relacionales.

La mayoría de los errores no se deben a la sintaxis, sino a una comprensión incorrecta de las relaciones entre tablas.

En este apartado analizaremos los errores más habituales y aprenderemos a detectarlos y corregirlos.

---

## Error 1. Olvidar la condición del JOIN

Es el error más peligroso.

```sql
SELECT
    *
FROM Cliente
CROSS JOIN Pedido;
```

o, utilizando la sintaxis antigua:

```sql
SELECT
    *
FROM Cliente,
     Pedido;
```

Si realmente no queremos un producto cartesiano, el resultado será enorme.

Supongamos:

* 2.000 clientes.
* 50.000 pedidos.

El resultado contendrá:

```text
100.000.000 filas
```

Este error puede bloquear fácilmente una base de datos de producción.

---

## Error 2. Relacionar columnas incorrectas

Supongamos las siguientes tablas:

```text
Cliente

IdCliente
Nombre

Producto

IdProducto
Nombre
```

Escribir:

```sql
SELECT
    *
FROM Cliente AS c
INNER JOIN Producto AS p
ON c.IdCliente = p.IdProducto;
```

puede ejecutarse correctamente, pero no tiene ningún sentido desde el punto de vista del modelo relacional.

La condición del `ON` debe unir columnas que realmente representen la misma relación.

---

## Error 3. Confundir INNER JOIN con LEFT JOIN

Muchos estudiantes utilizan siempre `INNER JOIN`.

Por ejemplo:

```sql
SELECT
    c.Nombre,
    p.IdPedido
FROM Cliente AS c
INNER JOIN Pedido AS p
ON c.IdCliente = p.IdCliente;
```

Si un cliente no tiene pedidos, desaparecerá del resultado.

Si queremos conservar todos los clientes debemos utilizar:

```sql
SELECT
    c.Nombre,
    p.IdPedido
FROM Cliente AS c
LEFT JOIN Pedido AS p
ON c.IdCliente = p.IdCliente;
```

Comprender esta diferencia es fundamental.

---

## Error 4. No utilizar alias

Una consulta extensa sin alias resulta difícil de leer.

```sql
SELECT
    Cliente.Nombre,
    Pedido.Fecha,
    Producto.Nombre
FROM Cliente
INNER JOIN Pedido
ON Cliente.IdCliente = Pedido.IdCliente
INNER JOIN Producto
ON ...
```

La misma consulta utilizando alias es mucho más clara.

```sql
SELECT
    c.Nombre,
    p.Fecha,
    pr.Nombre
FROM Cliente AS c
INNER JOIN Pedido AS p
ON c.IdCliente = p.IdCliente
INNER JOIN Producto AS pr
ON ...
```

---

## Error 5. Utilizar SELECT \*

Cuando intervienen varias tablas:

```sql
SELECT *
FROM Cliente
INNER JOIN Pedido
ON ...
```

pueden devolverse decenas de columnas.

Además, es frecuente que varias tablas tengan columnas con el mismo nombre (`Id`, `Nombre`, `Fecha`), dificultando la interpretación del resultado.

Es preferible seleccionar únicamente las columnas necesarias.

---

## Error 6. Duplicados inesperados

Muchos estudiantes creen que un `JOIN` siempre devuelve una única fila por registro.

No es cierto.

Si un cliente tiene cinco pedidos, aparecerá cinco veces.

Por ejemplo:

| Cliente | Pedido |
| --------- | -------- |
| Ana     | 101    |
| Ana     | 102    |
| Ana     | 103    |
| Ana     | 104    |
| Ana     | 105    |

Esto no es un error.

Simplemente refleja la relación uno a muchos existente entre ambas tablas.

---

## Error 7. No comprender la cardinalidad

Antes de escribir un `JOIN` conviene preguntarse:

* ¿Es una relación 1:1?
* ¿Es una relación 1:N?
* ¿Es una relación N:M?

La cardinalidad determina el número de filas que aparecerán en el resultado.

Ignorar este aspecto suele provocar consultas difíciles de interpretar.

---

## Error 8. No seguir el recorrido del modelo relacional

Supongamos que queremos obtener:

* cliente;
* categoría del producto.

Algunos estudiantes intentan unir directamente:

```text
Cliente

↓

Categoría
```

Sin embargo, ambas tablas no están relacionadas directamente.

El recorrido correcto sería:

```text
Cliente

↓

Pedido

↓

DetallePedido

↓

Producto

↓

Categoría
```

Seguir las relaciones del modelo evita la mayoría de los errores.

---

## Recomendaciones

Antes de ejecutar cualquier consulta con varios `JOIN` revisa siempre:

* las tablas utilizadas;
* la condición de cada `ON`;
* el tipo de `JOIN`;
* el número esperado de filas;
* la presencia de valores `NULL`;
* la existencia de duplicados esperados.

Una revisión de apenas unos segundos puede ahorrar mucho tiempo de depuración.

---

## Ideas clave

* El error más grave consiste en generar un producto cartesiano involuntario.
* La condición del `ON` debe relacionar correctamente las tablas.
* `INNER JOIN` y `LEFT JOIN` producen resultados diferentes.
* Los alias mejoran considerablemente la legibilidad.
* Comprender la cardinalidad ayuda a interpretar correctamente los resultados.

