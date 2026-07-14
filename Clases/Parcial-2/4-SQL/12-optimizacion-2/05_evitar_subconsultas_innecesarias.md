# Evitar subconsultas innecesarias

## Introducción

Las subconsultas constituyen una de las herramientas más potentes del lenguaje SQL.

Gracias a ellas es posible expresar problemas complejos de forma elegante y muy cercana al razonamiento humano.

Sin embargo, utilizar una subconsulta no significa automáticamente que estemos escribiendo la mejor solución.

En muchas ocasiones una subconsulta puede sustituirse por un `JOIN`, una vista o una reestructuración de la consulta que resulte más sencilla y eficiente.

El objetivo no es eliminar todas las subconsultas.

El objetivo consiste en identificar aquellas que no aportan ninguna ventaja y que únicamente incrementan la complejidad del código o dificultan el trabajo del optimizador.

## ¿Qué es una subconsulta?

Una subconsulta es una consulta incluida dentro de otra consulta.

Por ejemplo:

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

La consulta interior obtiene los identificadores de clientes con pedidos.

La consulta exterior utiliza ese resultado para recuperar los nombres.

La solución es correcta.

La cuestión es si existe una alternativa mejor.

## El mismo problema utilizando JOIN

Podemos escribir:

```sql
SELECT DISTINCT
    c.Nombre
FROM Cliente AS c
JOIN Pedido AS p
    ON c.IdCliente = p.IdCliente;
```

Ambas consultas producen el mismo resultado.

Dependiendo de los índices y del volumen de datos, el optimizador puede ejecutar una u otra de forma más eficiente.

## Subconsultas que se ejecutan repetidamente

Uno de los casos más problemáticos aparece con las subconsultas correlacionadas.

Ejemplo:

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

La subconsulta hace referencia a la consulta exterior.

Conceptualmente puede evaluarse una vez por cada cliente.

Aunque el optimizador moderno es capaz de transformar muchas de estas consultas, conviene conocer que pueden resultar más costosas.

## Evitar cálculos repetidos

Supongamos:

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

En este caso la subconsulta no depende de la consulta exterior.

El optimizador puede calcular la media una única vez.

Este tipo de subconsulta suele resultar perfectamente razonable.

No todas las subconsultas representan un problema.

## Subconsultas anidadas

A veces encontramos consultas como:

```sql
SELECT *
FROM Cliente
WHERE IdCliente IN
(
    SELECT IdCliente
    FROM Pedido
    WHERE IdEmpleado IN
    (
        SELECT IdEmpleado
        FROM Empleado
        WHERE Departamento = 'Ventas'
    )
);
```

Aunque son correctas, varias capas de anidamiento dificultan considerablemente la lectura.

En muchos casos una solución basada en `JOIN` resulta más clara.

## Comparación de legibilidad

Versión con varias subconsultas:

```sql
SELECT *
FROM Cliente
WHERE IdCliente IN
(
    SELECT IdCliente
    FROM Pedido
);
```

Versión con `JOIN`:

```sql
SELECT DISTINCT
    c.*
FROM Cliente AS c
JOIN Pedido AS p
    ON c.IdCliente = p.IdCliente;
```

No existe una regla absoluta.

En algunos escenarios la primera versión expresa mejor la lógica del problema.

En otros, la segunda resulta más natural.

## Pensar en el optimizador

El optimizador de MySQL es capaz de transformar numerosas subconsultas en operaciones equivalentes.

Sin embargo, esto no ocurre siempre.

Cuando una consulta presenta problemas de rendimiento conviene comprobar con `EXPLAIN` si la estructura elegida está siendo ejecutada de forma eficiente.

Nunca debe suponerse que una subconsulta será lenta o rápida sin analizar el plan de ejecución.

## ¿Cuándo mantener una subconsulta?

Una subconsulta suele ser una buena opción cuando:

- Expresa claramente la lógica del problema.
- Calcula un valor agregado.
- Produce un conjunto de resultados intermedio fácil de comprender.
- Su rendimiento es adecuado.

No debe eliminarse únicamente por seguir una regla general.

## ¿Cuándo plantearse otra alternativa?

Conviene revisar una subconsulta cuando:

- Existen muchos niveles de anidamiento.
- La lectura resulta complicada.
- El plan de ejecución muestra un elevado coste.
- Puede sustituirse por un `JOIN` mucho más claro.
- Se ejecuta repetidamente sobre un gran número de registros.

## Buenas prácticas

- Utilizar subconsultas cuando aporten claridad.
- Evitar anidamientos innecesarios.
- Comparar distintas alternativas con `EXPLAIN`.
- No asumir que un `JOIN` siempre será más rápido.
- Priorizar soluciones fáciles de comprender y mantener.

## Conclusiones

Las subconsultas son una herramienta fundamental del lenguaje SQL, pero deben utilizarse con criterio. En algunos casos representan la solución más elegante; en otros, una reescritura mediante `JOIN` o una reorganización de la consulta puede ofrecer un código más claro y un mejor rendimiento. La decisión debe basarse en el problema concreto y en el comportamiento observado del optimizador.

## Ideas clave

- Las subconsultas no son malas por definición.
- Algunas pueden sustituirse por soluciones más sencillas.
- Las subconsultas correlacionadas requieren especial atención.
- `EXPLAIN` permite comparar distintas alternativas.
- La claridad y el rendimiento deben evaluarse conjuntamente.

