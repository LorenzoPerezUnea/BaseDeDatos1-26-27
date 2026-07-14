# Índices compuestos

## Introducción

En el apartado anterior aprendimos a crear índices sobre una única columna.

Sin embargo, en aplicaciones reales muchas consultas filtran utilizando varias columnas al mismo tiempo.

Por ejemplo:

```sql
SELECT *
FROM Pedido
WHERE IdCliente = 25
  AND Estado = 'Pendiente';
```

O bien:

```sql
SELECT *
FROM Empleado
WHERE Departamento = 'Ventas'
  AND Ciudad = 'Madrid';
```

En estos casos podríamos pensar en crear un índice para cada columna.

```text
Índice sobre IdCliente

Índice sobre Estado
```

Sin embargo, existe otra alternativa que en muchas ocasiones resulta mucho más eficiente: **los índices compuestos**.

Estos índices almacenan varias columnas dentro de una única estructura B-Tree.

Comprender su funcionamiento es esencial para diseñar bases de datos de alto rendimiento.

## ¿Qué es un índice compuesto?

Un índice compuesto es un índice construido sobre varias columnas.

Por ejemplo:

```sql
CREATE INDEX idx_pedido_cliente_estado
ON Pedido
(
    IdCliente,
    Estado
);
```

En este caso el índice no almacena únicamente el identificador del cliente.

Cada entrada contiene la combinación de ambas columnas.

Conceptualmente sería algo parecido a:

```text
(IdCliente, Estado)

(1, Entregado)

(1, Pendiente)

(2, Cancelado)

(2, Pendiente)

(3, En preparación)
```

Los valores permanecen ordenados siguiendo el orden definido al crear el índice.

## ¿Por qué utilizar un índice compuesto?

Supongamos que una empresa consulta constantemente:

```sql
SELECT *
FROM Pedido
WHERE IdCliente = 120
AND Estado = 'Pendiente';
```

Si únicamente existe un índice sobre:

```text
IdCliente
```

MySQL localizará rápidamente todos los pedidos del cliente.

Después deberá revisar cuáles están pendientes.

Si existe un índice compuesto sobre:

```text
(IdCliente, Estado)
```

el motor puede localizar directamente los pedidos pendientes de ese cliente sin realizar filtrados adicionales.

Esto reduce considerablemente el número de registros leídos.

## El orden de las columnas importa

Uno de los aspectos más importantes de los índices compuestos es que **el orden de las columnas no es indiferente**.

Consideremos el siguiente índice.

```sql
CREATE INDEX idx_cliente_estado
ON Pedido
(
    IdCliente,
    Estado
);
```

Este índice está organizado primero por:

```
IdCliente
```

y, dentro de cada cliente, por:

```
Estado
```

No es equivalente a:

```sql
CREATE INDEX idx_estado_cliente
ON Pedido
(
    Estado,
    IdCliente
);
```

Aunque ambas estructuras contienen las mismas columnas, el árbol está organizado de forma distinta.

## La regla del prefijo izquierdo

Los índices compuestos siguen una regla muy importante conocida como **regla del prefijo izquierdo** (*Leftmost Prefix Rule*).

Significa que el índice puede aprovecharse siempre que la consulta utilice las primeras columnas del índice respetando su orden.

Supongamos el siguiente índice.

```sql
CREATE INDEX idx_cliente_estado_fecha
ON Pedido
(
    IdCliente,
    Estado,
    FechaPedido
);
```

Este índice puede utilizarse para consultas como:

```sql
WHERE IdCliente = 20
```

o bien:

```sql
WHERE IdCliente = 20
AND Estado = 'Pendiente'
```

o incluso:

```sql
WHERE IdCliente = 20
AND Estado = 'Pendiente'
AND FechaPedido >= '2026-01-01'
```

Sin embargo, una consulta como:

```sql
WHERE Estado = 'Pendiente'
```

no puede aprovechar correctamente este índice, ya que omite la primera columna.

## Ejemplos

### Consulta 1

```sql
SELECT *
FROM Pedido
WHERE IdCliente = 5;
```

Puede utilizar completamente el índice.

### Consulta 2

```sql
SELECT *
FROM Pedido
WHERE IdCliente = 5
AND Estado = 'Pendiente';
```

También puede utilizar el índice.

### Consulta 3

```sql
SELECT *
FROM Pedido
WHERE Estado = 'Pendiente';
```

Normalmente no podrá aprovechar el índice compuesto anterior.

## Índices y ORDER BY

Los índices compuestos también pueden acelerar determinadas ordenaciones.

Supongamos:

```sql
CREATE INDEX idx_categoria_precio
ON Producto
(
    Categoria,
    Precio
);
```

Consulta:

```sql
SELECT *
FROM Producto
WHERE Categoria = 'Monitores'
ORDER BY Precio;
```

Como el índice ya está ordenado primero por categoría y después por precio, MySQL puede devolver los resultados ordenados sin necesidad de realizar una ordenación adicional.

Este comportamiento supone una mejora importante cuando se trabaja con grandes volúmenes de datos.

## Índices y JOIN

Los índices compuestos también pueden mejorar algunos `JOIN`.

Por ejemplo, si una consulta combina varias condiciones sobre las mismas columnas que forman el índice, el optimizador puede utilizarlo para reducir considerablemente el número de comparaciones.

## ¿Cuántas columnas puede tener?

MySQL permite crear índices con numerosas columnas.

Sin embargo, en la práctica no suele ser recomendable construir índices excesivamente grandes.

Cada columna adicional:

- Incrementa el espacio ocupado.
- Aumenta el tiempo necesario para actualizar el índice.
- Hace más costosas las operaciones de escritura.

Lo habitual es crear índices compuestos con dos o tres columnas, seleccionadas cuidadosamente según las consultas más frecuentes.

## Cómo decidir el orden

Una regla práctica consiste en colocar primero las columnas:

- Más utilizadas en los filtros.
- Con mayor capacidad de discriminación.
- Más frecuentes en las consultas.

No existe una regla universal.

La decisión depende del uso real de la aplicación y debe apoyarse en el análisis del plan de ejecución.

## Buenas prácticas

- Diseñar índices pensando en consultas reales.
- Respetar la regla del prefijo izquierdo.
- Evitar índices compuestos innecesariamente largos.
- Analizar siempre el orden de las columnas.
- Verificar su utilización mediante `EXPLAIN`.

## Conclusiones

Los índices compuestos permiten optimizar consultas que utilizan varias columnas simultáneamente. Su eficacia depende en gran medida del orden de las columnas y del patrón de acceso de las consultas. Un diseño adecuado puede reducir de forma muy significativa el tiempo de ejecución en aplicaciones con grandes volúmenes de datos.

## Ideas clave

- Un índice compuesto incluye varias columnas en una única estructura.
- El orden de las columnas es fundamental.
- Se aplica la regla del prefijo izquierdo.
- También pueden mejorar `ORDER BY` y determinados `JOIN`.
- Deben diseñarse a partir de las consultas más habituales de la aplicación.

