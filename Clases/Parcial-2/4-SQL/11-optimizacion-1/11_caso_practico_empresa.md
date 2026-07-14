# Caso práctico empresarial

## Introducción

La empresa ficticia **TechShop**, utilizada a lo largo del curso, ha experimentado un importante crecimiento durante los últimos años.

Actualmente dispone de:

- 2 millones de clientes.
- 18 millones de pedidos.
- 75 millones de líneas de pedido.
- 450 000 productos.
- Más de 200 empleados accediendo simultáneamente al sistema.

Los usuarios comienzan a informar de que determinadas pantallas tardan demasiado tiempo en cargarse.

Nuestro objetivo será analizar varias consultas reales y proponer mejoras utilizando los conocimientos adquiridos en esta clase.

## Escenario 1. Búsqueda de clientes

Consulta original.

```sql
SELECT *
FROM Cliente
WHERE Email = 'ana.lopez@empresa.com';
```

La columna `Email` no posee ningún índice.

Plan simplificado.

| type | key | rows |
|------|-----|------:|
| ALL | NULL | 2000000 |

MySQL debe recorrer aproximadamente dos millones de registros.

### Solución

Crear un índice.

```sql
CREATE INDEX idx_cliente_email
ON Cliente (Email);
```

Nuevo plan.

| type | key | rows |
|------|-----|------:|
| ref | idx_cliente_email | 1 |

La diferencia es enorme.

Ahora el motor accede prácticamente de forma directa al registro buscado.

## Escenario 2. Pedidos por fecha

Consulta.

```sql
SELECT *
FROM Pedido
WHERE FechaPedido >= '2026-01-01';
```

La tabla contiene dieciocho millones de pedidos.

Inicialmente no existe ningún índice sobre la fecha.

Plan.

| type | rows |
|------|------:|
| ALL | 18000000 |

### Optimización

```sql
CREATE INDEX idx_pedido_fecha
ON Pedido (FechaPedido);
```

Nuevo plan.

| type | rows |
|------|------:|
| range | 185000 |

Aunque sigue siendo un número elevado, únicamente se recorren los registros pertenecientes al intervalo solicitado.

## Escenario 3. Consulta sobre clientes y pedidos

Consulta.

```sql
SELECT
    c.Nombre,
    p.FechaPedido
FROM Cliente c
JOIN Pedido p
ON c.IdCliente = p.IdCliente
WHERE c.Ciudad = 'Santander';
```

Existe un índice sobre:

```text
Pedido.IdCliente
```

pero no sobre:

```text
Cliente.Ciudad
```

El optimizador debe revisar un gran número de clientes antes de realizar el JOIN.

### Solución

```sql
CREATE INDEX idx_cliente_ciudad
ON Cliente (Ciudad);
```

Ahora el conjunto inicial de clientes se reduce considerablemente antes de combinar ambas tablas.

## Escenario 4. Uso incorrecto de funciones

Consulta.

```sql
SELECT *
FROM Pedido
WHERE YEAR(FechaPedido) = 2026;
```

Aunque existe un índice sobre `FechaPedido`, MySQL no puede aprovecharlo correctamente.

Reescribimos la consulta.

```sql
SELECT *
FROM Pedido
WHERE FechaPedido >= '2026-01-01'
AND FechaPedido < '2027-01-01';
```

Sin modificar los datos obtenidos, el optimizador puede utilizar el índice mediante un acceso de tipo `range`.

## Escenario 5. SELECT innecesariamente amplio

Consulta original.

```sql
SELECT *
FROM Producto
WHERE Categoria = 'Portátiles';
```

La aplicación únicamente muestra:

- Nombre.
- Precio.
- Stock.

Podemos escribir:

```sql
SELECT
    Nombre,
    Precio,
    Stock
FROM Producto
WHERE Categoria = 'Portátiles';
```

Se reduce la cantidad de información transferida y el consumo de memoria.

## Resultados obtenidos

Después de aplicar las optimizaciones:

- Se reducen los tiempos de respuesta.
- Disminuye el número de registros leídos.
- El servidor soporta un mayor número de usuarios simultáneos.
- Se reduce la carga sobre CPU y disco.
- La experiencia de los usuarios mejora de forma notable.

## Lecciones aprendidas

Este caso práctico muestra una idea fundamental:

La mayoría de los problemas de rendimiento no requieren hardware más potente.

En muchas ocasiones basta con:

- Crear el índice adecuado.
- Reescribir ligeramente una consulta.
- Analizar el plan de ejecución.
- Comprender cómo trabaja el optimizador.

## Buenas prácticas

- Analizar las consultas más utilizadas por la aplicación.
- Optimizar primero las consultas críticas.
- Verificar siempre las mejoras con `EXPLAIN`.
- Medir el rendimiento antes y después de cada cambio.
- Documentar las decisiones de optimización adoptadas.

## Conclusiones

La optimización de consultas es un proceso continuo que combina conocimiento del modelo de datos, comprensión del funcionamiento interno de MySQL y análisis del plan de ejecución. En un entorno empresarial, pequeñas mejoras pueden traducirse en importantes incrementos de rendimiento y en una mejor experiencia para los usuarios.

## Ideas clave

- Los índices deben responder a necesidades reales.
- `EXPLAIN` es imprescindible para validar una optimización.
- Reescribir una consulta puede ser tan eficaz como crear un índice.
- La optimización debe medirse, no suponerse.
- Un buen diseño permite que la aplicación siga siendo eficiente incluso cuando el volumen de datos crece de forma considerable.

