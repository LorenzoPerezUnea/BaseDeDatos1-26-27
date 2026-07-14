# Reescritura de consultas

## Introducción

Uno de los principios más importantes de la optimización consiste en comprender que **una misma necesidad puede expresarse de muchas formas distintas**.

El lenguaje SQL es declarativo.

Esto significa que indicamos **qué resultado queremos obtener**, pero no especificamos exactamente cómo debe conseguirlo.

Aun así, la forma en la que escribimos una consulta influye en:

- La facilidad con la que el optimizador puede analizarla.
- La claridad del código.
- El mantenimiento futuro.
- En algunos casos, el propio rendimiento.

Reescribir una consulta no significa cambiar el resultado.

Significa expresar la misma lógica de una forma más sencilla, más clara o más eficiente.

## ¿Qué significa reescribir una consulta?

Supongamos que queremos obtener los pedidos pendientes.

Primera versión.

```sql
SELECT *
FROM Pedido
WHERE Estado = 'Pendiente';
```

Otra versión equivalente.

```sql
SELECT *
FROM Pedido
WHERE Estado IN ('Pendiente');
```

Ambas devuelven exactamente el mismo resultado.

Sin embargo, la primera expresa de forma más directa lo que queremos hacer.

La reescritura busca precisamente eliminar complejidad innecesaria.

## Simplificar condiciones

A veces encontramos consultas como:

```sql
SELECT *
FROM Producto
WHERE Precio >= 100
AND Precio <= 500;
```

Podemos escribir:

```sql
SELECT *
FROM Producto
WHERE Precio BETWEEN 100 AND 500;
```

Las dos consultas son equivalentes.

La segunda suele resultar más fácil de leer.

## Eliminar condiciones redundantes

Consideremos el siguiente ejemplo.

```sql
SELECT *
FROM Cliente
WHERE Activo = 1
AND Activo = 1;
```

La segunda condición no aporta ninguna información adicional.

Una consulta más limpia sería:

```sql
SELECT *
FROM Cliente
WHERE Activo = 1;
```

Eliminar redundancias facilita la lectura y evita confusiones.

## Sustituir OR cuando sea posible

Supongamos:

```sql
SELECT *
FROM Producto
WHERE Categoria = 'Portátiles'
OR Categoria = 'Monitores';
```

Podemos escribir:

```sql
SELECT *
FROM Producto
WHERE Categoria IN
(
    'Portátiles',
    'Monitores'
);
```

La segunda versión resulta más compacta y facilita añadir nuevos valores.

## Evitar expresiones innecesarias

Consulta original.

```sql
SELECT *
FROM Pedido
WHERE NOT (Estado <> 'Pendiente');
```

Versión simplificada.

```sql
SELECT *
FROM Pedido
WHERE Estado = 'Pendiente';
```

La segunda consulta expresa exactamente la misma idea de forma mucho más clara.

## Reescribir operaciones con fechas

Consulta poco recomendable.

```sql
SELECT *
FROM Pedido
WHERE YEAR(FechaPedido) = 2026;
```

Consulta optimizada.

```sql
SELECT *
FROM Pedido
WHERE FechaPedido >= '2026-01-01'
AND FechaPedido < '2027-01-01';
```

Además de ser más eficiente al permitir el uso de índices, esta versión expresa explícitamente el intervalo de fechas utilizado.

## Dividir problemas complejos

Cuando una consulta contiene numerosas condiciones, puede ser conveniente reorganizarla.

Ejemplo.

```sql
SELECT
    c.Nombre,
    p.FechaPedido,
    p.Total
FROM Cliente AS c
JOIN Pedido AS p
    ON c.IdCliente = p.IdCliente
WHERE
    c.Activo = 1
    AND p.Estado = 'Pendiente'
    AND p.Total > 500
ORDER BY
    p.FechaPedido DESC;
```

La estructura por bloques facilita enormemente su comprensión.

## Eliminar cálculos repetidos

Consulta.

```sql
SELECT
    Precio,
    Precio * 1.21 AS PrecioConIVA
FROM Producto
WHERE Precio * 1.21 > 100;
```

Aquí el mismo cálculo aparece dos veces.

Dependiendo del contexto puede resultar conveniente reorganizar la consulta para evitar repeticiones y mejorar su claridad.

## Mantener la intención del código

Una buena reescritura no debe sorprender al siguiente desarrollador.

El objetivo consiste en que la consulta explique claramente qué pretende hacer.

Cuando una optimización hace que el código resulte muy difícil de comprender, conviene valorar si realmente compensa.

## Reescribir pensando en el futuro

Las consultas rara vez permanecen invariables.

Con el tiempo suelen añadirse:

- Nuevos filtros.
- Nuevas columnas.
- Nuevos JOIN.
- Nuevas reglas de negocio.

Una consulta organizada facilita estas modificaciones.

## Buenas prácticas

- Simplificar expresiones cuando sea posible.
- Eliminar condiciones redundantes.
- Evitar cálculos repetidos.
- Organizar claramente las cláusulas.
- Mantener siempre la claridad del código.
- Comprobar con `EXPLAIN` que la nueva versión mantiene o mejora el rendimiento.

## Conclusiones

Reescribir una consulta no consiste únicamente en hacerla más rápida. También implica mejorar su legibilidad, facilitar su mantenimiento y permitir que el optimizador pueda analizarla con mayor facilidad. Una consulta sencilla suele ser más fácil de entender, modificar y optimizar.

## Ideas clave

- Varias consultas pueden expresar la misma lógica.
- La simplicidad favorece la legibilidad.
- Las expresiones redundantes deben eliminarse.
- Una buena reescritura mantiene exactamente el mismo resultado.
- Toda modificación debe comprobarse mediante mediciones objetivas.

