# Optimización de ORDER BY

## Introducción

Ordenar información es una de las operaciones más habituales en cualquier aplicación informática.

Cuando un usuario consulta un catálogo de productos, normalmente espera verlos ordenados por nombre, precio o categoría. En una tienda en línea es frecuente ordenar por precio ascendente o descendente. En un sistema de gestión empresarial se ordenan pedidos por fecha o empleados por apellido.

Todo ello se consigue mediante la cláusula:

```sql
ORDER BY
```

Aunque su utilización es muy sencilla, ordenar grandes cantidades de información puede convertirse en una de las operaciones más costosas de una consulta.

Comprender cómo optimizar `ORDER BY` permite reducir tiempos de ejecución y evitar consumos innecesarios de memoria y disco.

## ¿Cómo ordena MySQL los datos?

Cuando MySQL recibe una consulta con `ORDER BY`, tiene dos posibilidades principales:

- Utilizar un índice que ya contiene la información ordenada.
- Realizar una ordenación adicional durante la ejecución.

La primera opción suele ser mucho más rápida.

La segunda requiere procesar todos los registros antes de devolver el resultado.

Por ello, uno de los objetivos del optimizador consiste en evitar ordenaciones innecesarias.

## Ordenar utilizando un índice

Supongamos la tabla:

```text
Producto
```

y el índice:

```sql
CREATE INDEX idx_producto_nombre
ON Producto(Nombre);
```

Consulta:

```sql
SELECT
    Nombre,
    Precio
FROM Producto
ORDER BY Nombre;
```

En este caso MySQL puede recorrer directamente el índice.

No necesita reorganizar posteriormente los registros.

Esta estrategia suele ser muy eficiente.

## Cuando no existe un índice

Si ejecutamos:

```sql
SELECT
    Nombre,
    Precio
FROM Producto
ORDER BY Precio;
```

y no existe un índice sobre `Precio`, MySQL deberá ordenar todos los registros durante la ejecución.

En tablas pequeñas la diferencia apenas será apreciable.

En tablas con millones de filas el coste puede ser considerable.

## Ordenar solo cuando sea necesario

Un error relativamente frecuente consiste en ordenar resultados que posteriormente no necesitan mantenerse ordenados.

Por ejemplo:

```sql
SELECT *
FROM Producto
ORDER BY Nombre;
```

si la aplicación vuelve a ordenar los datos posteriormente o simplemente procesa cada fila sin importar el orden, la operación resulta innecesaria.

Cada `ORDER BY` debe responder a una necesidad real.

## Combinar ORDER BY y LIMIT

Una combinación muy habitual es:

```sql
SELECT
    Nombre,
    Precio
FROM Producto
ORDER BY Precio DESC
LIMIT 10;
```

El objetivo consiste en obtener únicamente los diez productos más caros.

Si existe un índice adecuado, MySQL puede localizar rápidamente los primeros registros sin ordenar toda la tabla.

Esta técnica es muy utilizada en aplicaciones web.

## Evitar ordenar columnas calculadas

Consulta:

```sql
SELECT
    Nombre,
    Precio * 1.21 AS PrecioConIVA
FROM Producto
ORDER BY Precio * 1.21;
```

La expresión debe calcularse para cada registro antes de realizar la ordenación.

Siempre que sea posible resulta preferible ordenar utilizando columnas existentes.

## ORDER BY sobre varias columnas

También es frecuente ordenar por varios criterios.

```sql
SELECT
    Nombre,
    Categoria,
    Precio
FROM Producto
ORDER BY
    Categoria,
    Precio;
```

En este caso un índice compuesto sobre:

```text
Categoria,
Precio
```

puede resultar especialmente útil.

Como siempre, el orden de las columnas del índice debe coincidir con el patrón de consulta más habitual.

## Comprobar el plan de ejecución

Mediante:

```sql
EXPLAIN
```

podemos observar si MySQL necesita realizar operaciones adicionales de ordenación.

En la columna `Extra` pueden aparecer mensajes relacionados con la utilización de procesos de ordenación.

Cuando esto sucede conviene revisar la consulta y la estrategia de indexación.

## Caso práctico

La empresa TechShop muestra continuamente el catálogo de productos ordenado por nombre.

Consulta:

```sql
SELECT
    Nombre,
    Precio,
    Stock
FROM Producto
ORDER BY Nombre;
```

La tabla contiene cinco millones de productos.

Sin un índice sobre `Nombre`, cada consulta obliga a ordenar toda la información.

La creación de un índice adecuado puede reducir enormemente el tiempo de respuesta.

## Buenas prácticas

- Ordenar únicamente cuando sea necesario.
- Crear índices para las columnas utilizadas frecuentemente en `ORDER BY`.
- Combinar `ORDER BY` y `LIMIT` cuando solo se necesitan los primeros resultados.
- Evitar ordenar expresiones calculadas si existe una alternativa equivalente.
- Analizar siempre el comportamiento mediante `EXPLAIN`.

## Conclusiones

`ORDER BY` es una herramienta esencial para presentar información al usuario, pero también puede convertirse en una operación costosa. Diseñar correctamente los índices y evitar ordenaciones innecesarias permite mejorar significativamente el rendimiento de muchas aplicaciones.

## Ideas clave

- Ordenar información tiene un coste.
- Los índices permiten evitar muchas operaciones de ordenación.
- `ORDER BY` debe utilizarse únicamente cuando sea necesario.
- La combinación con `LIMIT` puede ser especialmente eficiente.
- `EXPLAIN` ayuda a comprobar cómo resuelve MySQL la ordenación.

