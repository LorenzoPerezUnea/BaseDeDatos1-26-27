# Optimización de consultas

## Introducción

Una vez comprendido cómo trabaja el optimizador de MySQL, qué son los índices y cómo interpretar un plan de ejecución mediante `EXPLAIN`, estamos preparados para abordar el verdadero objetivo de este tema: **mejorar el rendimiento de las consultas**.

Optimizar una consulta no significa escribir SQL "más bonito" o utilizar menos líneas de código.

Una consulta optimizada es aquella que:

- Devuelve exactamente el mismo resultado.
- Consume menos CPU.
- Lee menos páginas de disco.
- Utiliza menos memoria.
- Finaliza en menos tiempo.
- Escala correctamente cuando el volumen de datos aumenta.

En aplicaciones empresariales con millones de registros, pequeñas mejoras pueden suponer un ahorro de varios segundos por consulta y miles de horas de procesamiento a lo largo del año.

## El primer principio: medir antes de modificar

Un error muy frecuente consiste en comenzar a cambiar consultas por intuición.

Por ejemplo, un desarrollador puede pensar:

> "Creo que esta consulta es lenta."

Antes de modificar nada debemos comprobarlo.

Las herramientas básicas son:

```sql
EXPLAIN
```

y

```sql
EXPLAIN ANALYZE
```

(si la versión de MySQL lo permite).

Solo con datos objetivos podremos saber si realmente existe un problema.

## Optimizar no siempre significa añadir índices

Supongamos la siguiente consulta.

```sql
SELECT *
FROM Cliente;
```

Si la aplicación necesita mostrar todos los clientes, un índice no mejorará prácticamente nada.

El problema no es la ausencia de índices.

El problema es que estamos solicitando todos los registros.

En ocasiones la mejor optimización consiste en modificar la propia consulta.

## Evitar SELECT *

Una de las recomendaciones más conocidas consiste en evitar:

```sql
SELECT *
```

cuando no sea necesario.

Por ejemplo:

```sql
SELECT *
FROM Producto;
```

Si únicamente necesitamos el nombre y el precio, resulta preferible escribir:

```sql
SELECT
    Nombre,
    Precio
FROM Producto;
```

Las ventajas son:

- Menor cantidad de datos transferidos.
- Menor uso de memoria.
- Menor tráfico por la red.
- Mejor aprovechamiento de algunos índices.

## Filtrar cuanto antes

Cuanto antes pueda reducir MySQL el número de registros, menos trabajo tendrá que realizar.

Consulta poco eficiente:

```sql
SELECT *
FROM Pedido;
```

Consulta mucho mejor:

```sql
SELECT *
FROM Pedido
WHERE Estado = 'Pendiente';
```

El filtro reduce considerablemente el número de filas procesadas.

## Aprovechar los índices

Supongamos un índice sobre:

```text
FechaPedido
```

Consulta adecuada.

```sql
SELECT *
FROM Pedido
WHERE FechaPedido >= '2026-01-01';
```

El optimizador puede recorrer únicamente el rango necesario del índice.

En cambio:

```sql
SELECT *
FROM Pedido
WHERE YEAR(FechaPedido) = 2026;
```

Aquí aparece un problema importante.

## Evitar funciones sobre columnas indexadas

Cuando aplicamos una función directamente sobre una columna indexada, muchas veces el índice deja de ser útil.

Ejemplo poco recomendable:

```sql
SELECT *
FROM Pedido
WHERE YEAR(FechaPedido) = 2026;
```

Alternativa mucho mejor:

```sql
SELECT *
FROM Pedido
WHERE FechaPedido >= '2026-01-01'
AND FechaPedido < '2027-01-01';
```

El resultado es exactamente el mismo.

Sin embargo, ahora MySQL puede utilizar el índice sobre `FechaPedido`.

## Evitar cálculos innecesarios

Otro ejemplo.

```sql
WHERE Precio * 1.21 > 100
```

Es preferible transformar la expresión.

```sql
WHERE Precio > 100 / 1.21
```

Así el índice sobre `Precio` puede seguir siendo utilizado.

## Cuidado con LIKE

Recordemos que los índices B-Tree están ordenados desde el comienzo del valor.

Consulta eficiente.

```sql
WHERE Nombre LIKE 'Mar%'
```

Consulta poco eficiente.

```sql
WHERE Nombre LIKE '%Mar%'
```

En el segundo caso MySQL normalmente deberá revisar todos los registros.

## Limitar resultados

Cuando solo necesitamos unas pocas filas, resulta recomendable utilizar:

```sql
LIMIT
```

Por ejemplo:

```sql
SELECT *
FROM Producto
ORDER BY Precio DESC
LIMIT 20;
```

Esto evita procesar y transferir una cantidad innecesaria de información.

## Elegir correctamente las columnas del JOIN

Los `JOIN` deberían realizarse sobre columnas indexadas.

Por ejemplo:

```sql
SELECT
    c.Nombre,
    p.FechaPedido
FROM Cliente c
JOIN Pedido p
ON c.IdCliente = p.IdCliente;
```

Si `IdCliente` posee un índice en ambas tablas, el rendimiento será mucho mejor.

## Analizar el número de filas

Supongamos el siguiente plan.

| type | rows |
|------|------:|
| ALL | 12000000 |

Claramente existe margen de mejora.

Después de crear un índice obtenemos:

| type | rows |
|------|------:|
| ref | 250 |

La reducción del trabajo realizado por MySQL es enorme.

Este tipo de comparaciones permite cuantificar la mejora obtenida.

## Un proceso sistemático

En un entorno profesional la optimización suele seguir un proceso similar al siguiente:

1. Detectar la consulta lenta.
2. Ejecutar `EXPLAIN`.
3. Analizar el plan de ejecución.
4. Identificar el cuello de botella.
5. Modificar la consulta o los índices.
6. Ejecutar nuevamente `EXPLAIN`.
7. Comparar resultados.
8. Medir tiempos reales.

Este enfoque evita optimizaciones basadas únicamente en suposiciones.

## Buenas prácticas

- Medir siempre antes de optimizar.
- Evitar `SELECT *` cuando no sea necesario.
- Escribir filtros que permitan utilizar índices.
- Evitar funciones sobre columnas indexadas.
- Revisar siempre el plan de ejecución después de realizar cambios.

## Conclusiones

La optimización de consultas es un proceso de análisis y mejora continua. No existen recetas universales; cada consulta debe estudiarse en función de sus datos, sus índices y su plan de ejecución. La combinación de un buen diseño SQL y un uso adecuado de `EXPLAIN` permite obtener mejoras significativas en el rendimiento de una base de datos.

## Ideas clave

- Optimizar consiste en reducir el trabajo realizado por MySQL.
- Las decisiones deben basarse en mediciones objetivas.
- Un índice no siempre resuelve un problema de rendimiento.
- Evitar funciones que impidan utilizar índices.
- El plan de ejecución debe analizarse antes y después de cualquier modificación.

