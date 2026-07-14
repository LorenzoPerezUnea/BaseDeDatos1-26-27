# Optimización de GROUP BY

## Introducción

La cláusula `GROUP BY` permite agrupar registros y calcular información resumida mediante funciones de agregación como:

- `COUNT()`
- `SUM()`
- `AVG()`
- `MIN()`
- `MAX()`

Es una de las herramientas más utilizadas para generar informes y estadísticas.

Sin embargo, también puede convertirse en una operación costosa cuando trabaja sobre tablas con millones de registros.

Comprender cómo optimizar las consultas que utilizan `GROUP BY` resulta fundamental en aplicaciones empresariales.

## ¿Cómo trabaja GROUP BY?

Supongamos la siguiente consulta.

```sql
SELECT
    Categoria,
    COUNT(*) AS TotalProductos
FROM Producto
GROUP BY Categoria;
```

MySQL debe recorrer los registros y agrupar todos aquellos que pertenecen a la misma categoría.

Posteriormente calcula el número de productos de cada grupo.

Cuantos más registros existan, mayor será el trabajo necesario.

## Reducir el número de filas antes de agrupar

Una regla muy importante consiste en filtrar los datos antes de realizar el agrupamiento.

Consulta poco eficiente.

```sql
SELECT
    Categoria,
    COUNT(*)
FROM Producto
GROUP BY Categoria;
```

Consulta más eficiente cuando solo interesan los productos activos.

```sql
SELECT
    Categoria,
    COUNT(*)
FROM Producto
WHERE Activo = 1
GROUP BY Categoria;
```

El filtro reduce el número de registros que participan en el agrupamiento.

## Utilizar índices adecuados

Si la columna utilizada en `GROUP BY` dispone de un índice, MySQL puede simplificar parte del trabajo.

Ejemplo.

```sql
CREATE INDEX idx_producto_categoria
ON Producto(Categoria);
```

Consulta.

```sql
SELECT
    Categoria,
    COUNT(*)
FROM Producto
GROUP BY Categoria;
```

Dependiendo del caso, el optimizador podrá aprovechar el orden existente en el índice.

## Agrupar únicamente por las columnas necesarias

Consulta poco recomendable.

```sql
GROUP BY
    Categoria,
    Precio,
    FechaAlta,
    Stock,
    Proveedor
```

Cada columna adicional incrementa el número de posibles grupos.

Cuando únicamente necesitamos agrupar por categoría, añadir otras columnas complica innecesariamente el proceso.

## Evitar cálculos innecesarios

Supongamos:

```sql
SELECT
    YEAR(FechaPedido),
    COUNT(*)
FROM Pedido
GROUP BY YEAR(FechaPedido);
```

La función debe calcular el año para cada registro.

En determinadas situaciones puede resultar preferible almacenar previamente cierta información o utilizar estrategias alternativas, especialmente cuando el volumen de datos es muy elevado.

## GROUP BY y ORDER BY

Una consulta como:

```sql
SELECT
    Categoria,
    COUNT(*)
FROM Producto
GROUP BY Categoria
ORDER BY Categoria;
```

puede aprovechar el mismo criterio de agrupación para devolver los resultados ordenados.

Sin embargo:

```sql
ORDER BY COUNT(*)
```

requiere un procesamiento adicional.

Conviene revisar siempre el plan de ejecución.

## Evitar agrupar información innecesaria

Antes de escribir una consulta debemos preguntarnos:

> ¿Necesitamos realmente agrupar todos los registros?

En ocasiones basta con aplicar un filtro previo.

Por ejemplo:

```sql
WHERE FechaPedido >= '2026-01-01'
```

reduce considerablemente el trabajo necesario.

## Analizar el plan de ejecución

Las consultas con `GROUP BY` deben comprobarse mediante:

```sql
EXPLAIN
```

Esto permite detectar:

- Tablas temporales.
- Ordenaciones adicionales.
- Escaneos completos.
- Índices desaprovechados.

## Caso práctico

Consulta.

```sql
SELECT
    IdCliente,
    SUM(Total)
FROM Pedido
GROUP BY IdCliente;
```

La tabla contiene veinte millones de pedidos.

Crear un índice sobre:

```text
IdCliente
```

puede mejorar significativamente el rendimiento del agrupamiento.

No obstante, siempre debe verificarse mediante el plan de ejecución.

## Buenas prácticas

- Filtrar antes de agrupar.
- Agrupar únicamente por las columnas necesarias.
- Aprovechar índices cuando sea posible.
- Revisar el plan de ejecución.
- Evitar cálculos repetidos dentro del `GROUP BY`.

## Conclusiones

`GROUP BY` es una herramienta imprescindible para obtener información resumida, pero puede convertirse en una operación costosa sobre grandes volúmenes de datos. Una buena estrategia consiste en reducir previamente el número de registros, aprovechar índices adecuados y comprobar siempre el comportamiento del optimizador mediante `EXPLAIN`.

## Ideas clave

- `GROUP BY` organiza los registros en grupos.
- Filtrar previamente reduce el coste del agrupamiento.
- Los índices pueden mejorar determinadas consultas.
- Conviene agrupar únicamente por las columnas necesarias.
- `EXPLAIN` permite analizar el comportamiento real de la consulta.

