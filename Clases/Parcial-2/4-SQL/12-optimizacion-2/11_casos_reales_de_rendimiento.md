# Casos reales de rendimiento

## Introducción

Hasta ahora hemos estudiado técnicas individuales para optimizar consultas SQL.

Sin embargo, en un entorno profesional los problemas de rendimiento rara vez aparecen de forma aislada.

Lo habitual es encontrar consultas desarrolladas hace años, modificadas por distintos programadores y ejecutándose sobre bases de datos que han crecido enormemente con el paso del tiempo.

En este apartado analizaremos varios casos inspirados en situaciones reales para comprender cómo pequeños cambios pueden producir mejoras muy importantes.

El objetivo no es memorizar soluciones concretas, sino aprender una metodología de análisis.

## Caso 1. Uso innecesario de SELECT *

Una aplicación mostraba un listado de clientes.

Consulta original:

```sql
SELECT *
FROM Cliente;
```

La tabla contenía:

- Datos personales.
- Dirección completa.
- Fotografía.
- Documentación digitalizada.
- Observaciones.
- Información fiscal.

Sin embargo, la pantalla únicamente mostraba:

- Nombre.
- Ciudad.
- Teléfono.

Consulta optimizada:

```sql
SELECT
    Nombre,
    Ciudad,
    Telefono
FROM Cliente;
```

La cantidad de datos transferidos disminuyó considerablemente.

## Caso 2. Función sobre una columna indexada

Consulta original:

```sql
SELECT *
FROM Pedido
WHERE YEAR(FechaPedido) = 2026;
```

La columna `FechaPedido` estaba indexada.

Sin embargo, la función `YEAR()` impedía aprovechar dicho índice.

Consulta optimizada:

```sql
SELECT *
FROM Pedido
WHERE FechaPedido >= '2026-01-01'
AND FechaPedido < '2027-01-01';
```

El índice volvió a utilizarse y el tiempo de ejecución se redujo de forma notable.

## Caso 3. Índices innecesarios

Una tabla disponía de índices sobre prácticamente todas sus columnas.

Cada inserción obligaba a actualizar una gran cantidad de estructuras.

Tras analizar las consultas ejecutadas por la aplicación se comprobó que varios índices nunca eran utilizados.

Su eliminación redujo significativamente el coste de las operaciones de escritura.

## Caso 4. JOIN sin índices

Consulta:

```sql
SELECT
    c.Nombre,
    p.FechaPedido
FROM Cliente AS c
JOIN Pedido AS p
    ON c.IdCliente = p.IdCliente;
```

La tabla `Pedido` no tenía índice sobre `IdCliente`.

Cada ejecución requería recorrer una gran cantidad de registros.

La creación del índice adecuado mejoró drásticamente el rendimiento.

## Caso 5. ORDER BY sobre millones de registros

Una aplicación mostraba productos ordenados por precio.

```sql
SELECT
    Nombre,
    Precio
FROM Producto
ORDER BY Precio;
```

La tabla superaba los diez millones de filas.

Tras crear un índice sobre `Precio`, el tiempo de respuesta disminuyó considerablemente.

## Caso 6. GROUP BY sin filtrado

Consulta original:

```sql
SELECT
    Categoria,
    COUNT(*)
FROM Producto
GROUP BY Categoria;
```

El informe únicamente necesitaba los productos activos.

Consulta optimizada:

```sql
SELECT
    Categoria,
    COUNT(*)
FROM Producto
WHERE Activo = 1
GROUP BY Categoria;
```

Reducir previamente el número de registros disminuyó el coste del agrupamiento.

## Caso 7. Consulta difícil de mantener

Consulta original:

```sql
SELECT c.Nombre,p.FechaPedido,e.Nombre
FROM Cliente c
JOIN Pedido p ON c.IdCliente=p.IdCliente
JOIN Empleado e ON e.IdEmpleado=p.IdEmpleado;
```

Aunque el rendimiento era correcto, la legibilidad resultaba escasa.

Versión refactorizada:

```sql
SELECT
    cli.Nombre,
    ped.FechaPedido,
    emp.Nombre
FROM Cliente AS cli
JOIN Pedido AS ped
    ON cli.IdCliente = ped.IdCliente
JOIN Empleado AS emp
    ON emp.IdEmpleado = ped.IdEmpleado;
```

El comportamiento no cambió, pero el mantenimiento se volvió mucho más sencillo.

## Enseñanzas comunes

En todos los casos anteriores aparecen varios principios repetidos.

- Recuperar únicamente la información necesaria.
- Aprovechar correctamente los índices.
- Evitar funciones que dificulten su utilización.
- Escribir consultas fáciles de comprender.
- Medir siempre antes de optimizar.

Estos principios son mucho más útiles que memorizar soluciones concretas.

## Metodología de trabajo

Ante un problema de rendimiento resulta recomendable seguir siempre el mismo procedimiento:

1. Confirmar que realmente existe un problema.
2. Medir tiempos de ejecución.
3. Analizar el plan mediante `EXPLAIN`.
4. Identificar el cuello de botella.
5. Aplicar una única mejora.
6. Volver a medir.
7. Comparar los resultados.

Este enfoque evita optimizaciones innecesarias y facilita identificar qué cambios producen realmente una mejora.

## Buenas prácticas

- Basar todas las decisiones en mediciones.
- Analizar primero las consultas más utilizadas.
- Optimizar progresivamente.
- Documentar los cambios realizados.
- Revisar periódicamente el rendimiento de la aplicación.

## Conclusiones

Los problemas reales de rendimiento rara vez se resuelven con una única técnica. Normalmente requieren combinar un buen diseño de índices, consultas bien escritas y un análisis cuidadoso del comportamiento del optimizador. La experiencia demuestra que pequeñas mejoras acumuladas producen grandes beneficios en sistemas de gran tamaño.

## Ideas clave

- Los problemas reales suelen tener múltiples causas.
- Optimizar requiere medir antes y después de cada cambio.
- La claridad del código también influye en el mantenimiento.
- Los índices deben responder al uso real de la aplicación.
- Una metodología sistemática produce mejores resultados que las optimizaciones basadas en intuiciones.

