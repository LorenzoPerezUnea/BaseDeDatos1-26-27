# JOIN vs Subconsulta

## Introducción

Uno de los debates más frecuentes entre desarrolladores SQL es el siguiente:

> ¿Es mejor utilizar un `JOIN` o una subconsulta?

La respuesta corta es muy sencilla:

**Depende del problema.**

No existe una regla universal que permita afirmar que una técnica sea siempre más rápida que la otra.

El rendimiento depende de numerosos factores:

- El volumen de datos.
- Los índices disponibles.
- El optimizador de MySQL.
- La estructura concreta de la consulta.
- Las estadísticas de la base de datos.

Por ello resulta más útil comprender las ventajas e inconvenientes de cada alternativa que intentar memorizar reglas absolutas.

## El mismo problema con dos enfoques

Supongamos que queremos obtener todos los clientes que han realizado pedidos.

Primera solución.

```sql
SELECT
    Nombre
FROM Cliente
WHERE IdCliente IN
(
    SELECT IdCliente
    FROM Pedido
);
```

Segunda solución.

```sql
SELECT DISTINCT
    c.Nombre
FROM Cliente AS c
JOIN Pedido AS p
    ON c.IdCliente = p.IdCliente;
```

Ambas producen el mismo resultado.

La diferencia se encuentra en la forma de expresar el problema.

## ¿Cuándo resulta natural una subconsulta?

Las subconsultas suelen expresar muy bien preguntas del tipo:

- Clientes que han realizado pedidos.
- Productos cuyo precio supera la media.
- Empleados con el salario máximo.
- Pedidos superiores al promedio.

Por ejemplo:

```sql
SELECT
    Nombre
FROM Producto
WHERE Precio >
(
    SELECT AVG(Precio)
    FROM Producto
);
```

La lógica resulta muy cercana al lenguaje natural.

## ¿Cuándo resulta natural un JOIN?

Los `JOIN` destacan cuando necesitamos combinar información procedente de varias tablas.

Ejemplo:

```sql
SELECT
    c.Nombre,
    p.FechaPedido
FROM Cliente AS c
JOIN Pedido AS p
    ON c.IdCliente = p.IdCliente;
```

Aquí el objetivo consiste precisamente en unir datos relacionados.

El uso de un `JOIN` resulta completamente natural.

## Legibilidad

Comparemos ambos enfoques.

Subconsulta.

```sql
SELECT
    Nombre
FROM Cliente
WHERE IdCliente IN
(
    SELECT IdCliente
    FROM Pedido
);
```

JOIN.

```sql
SELECT DISTINCT
    c.Nombre
FROM Cliente AS c
JOIN Pedido AS p
    ON c.IdCliente = p.IdCliente;
```

Dependiendo del problema, uno u otro puede resultar más fácil de comprender.

No existe una única respuesta correcta.

## Rendimiento

Durante muchos años era habitual afirmar que los `JOIN` siempre eran más rápidos.

Actualmente esta afirmación ya no puede considerarse válida.

El optimizador de MySQL es capaz de transformar numerosas subconsultas en operaciones equivalentes utilizando internamente estrategias similares a un `JOIN`.

Por ello dos consultas escritas de forma distinta pueden terminar ejecutándose prácticamente igual.

La única forma fiable de comparar ambas alternativas consiste en utilizar:

```sql
EXPLAIN
```

y medir tiempos reales.

## Subconsultas correlacionadas

Debe prestarse especial atención a las subconsultas correlacionadas.

Ejemplo.

```sql
SELECT
    Nombre
FROM Cliente AS c
WHERE EXISTS
(
    SELECT *
    FROM Pedido AS p
    WHERE p.IdCliente = c.IdCliente
);
```

La consulta interior depende de cada fila procesada por la consulta exterior.

En algunos escenarios esto puede incrementar el coste de ejecución.

Aunque el optimizador moderno puede aplicar transformaciones, conviene revisar siempre el plan de ejecución.

## Complejidad del código

Cuando una consulta contiene muchas tablas relacionadas, un único `JOIN` suele resultar más sencillo que una gran cantidad de subconsultas anidadas.

Por el contrario, cuando necesitamos calcular un único valor agregado, una subconsulta puede expresar mejor la intención.

## Elegir la herramienta adecuada

No debemos plantearnos la pregunta:

> ¿Qué técnica es más rápida?

Sino:

> ¿Qué técnica expresa mejor el problema y ofrece un buen rendimiento?

En muchos casos ambas respuestas coincidirán.

En otros será necesario comparar varias alternativas.

## Buenas prácticas

- Elegir la solución más clara.
- Utilizar `JOIN` para combinar información relacionada.
- Utilizar subconsultas cuando expresen mejor la lógica del problema.
- Analizar siempre el plan de ejecución.
- Evitar decisiones basadas en mitos o reglas absolutas.

## Conclusiones

`JOIN` y subconsultas son herramientas complementarias del lenguaje SQL. Ninguna de ellas es universalmente superior. La decisión debe basarse en la claridad del código, el comportamiento observado mediante `EXPLAIN` y las necesidades concretas de la aplicación.

## Ideas clave

- No existe una respuesta universal sobre qué técnica es mejor.
- Los `JOIN` son ideales para combinar tablas relacionadas.
- Las subconsultas expresan muy bien determinados problemas lógicos.
- El optimizador puede transformar ambas estrategias.
- Las decisiones deben apoyarse en mediciones y no en suposiciones.

