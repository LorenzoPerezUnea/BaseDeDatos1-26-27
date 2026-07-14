# Uso correcto de índices

## Introducción

En la clase anterior estudiamos en profundidad qué son los índices, cómo funcionan internamente y cómo permiten acelerar las búsquedas en una base de datos.

Sin embargo, disponer de índices no garantiza automáticamente un buen rendimiento.

Un índice únicamente resulta útil cuando:

- Está diseñado para responder a las consultas reales de la aplicación.
- El optimizador decide utilizarlo.
- La consulta está escrita de forma que pueda aprovecharlo.

Es habitual encontrar bases de datos con decenas de índices que apenas aportan mejoras porque fueron creados sin un análisis previo.

En este apartado estudiaremos cómo utilizar correctamente los índices dentro del desarrollo diario de aplicaciones SQL.

## Pensar primero en las consultas

El error más frecuente consiste en diseñar índices pensando únicamente en la estructura de la tabla.

Por ejemplo:

```text
Cliente

Nombre

Ciudad

Telefono

Email

FechaAlta

Activo
```

Un desarrollador podría decidir crear un índice sobre cada columna.

Aunque técnicamente es posible, probablemente no sea la mejor decisión.

Los índices deben diseñarse respondiendo a preguntas como:

- ¿Qué consultas ejecuta la aplicación con mayor frecuencia?
- ¿Qué columnas aparecen en las cláusulas `WHERE`?
- ¿Qué tablas participan en los `JOIN`?
- ¿Qué columnas se utilizan para ordenar?

Los índices deben reflejar el patrón de acceso a los datos.

## Aprovechar las claves existentes

Las claves primarias ya poseen un índice.

También ocurre habitualmente con las restricciones `UNIQUE`.

Por ejemplo:

```sql
CREATE TABLE Cliente
(
    IdCliente INT PRIMARY KEY,
    Email VARCHAR(200) UNIQUE,
    Nombre VARCHAR(100)
);
```

En este caso no tendría sentido crear:

```sql
CREATE INDEX idx_cliente_id
ON Cliente(IdCliente);
```

ni tampoco:

```sql
CREATE INDEX idx_cliente_email
ON Cliente(Email);
```

Ambos índices ya existen.

## Indexar columnas utilizadas en búsquedas

Supongamos que una aplicación busca continuamente clientes por correo electrónico.

```sql
SELECT *
FROM Cliente
WHERE Email = 'ana@empresa.com';
```

Un índice sobre:

```text
Email
```

puede reducir enormemente el tiempo de respuesta.

En cambio, si la columna nunca aparece en consultas, el índice apenas aportará beneficios.

## Indexar columnas utilizadas en JOIN

Los `JOIN` constituyen una de las operaciones más frecuentes en bases de datos relacionales.

Ejemplo:

```sql
SELECT
    c.Nombre,
    p.FechaPedido
FROM Cliente AS c
JOIN Pedido AS p
    ON c.IdCliente = p.IdCliente;
```

La existencia de índices sobre las columnas utilizadas para relacionar ambas tablas facilita enormemente el trabajo del optimizador.

En aplicaciones empresariales esta práctica resulta prácticamente imprescindible.

## Aprovechar índices compuestos

Consideremos las siguientes consultas frecuentes.

```sql
SELECT *
FROM Pedido
WHERE IdCliente = 120
AND Estado = 'Pendiente';
```

Un índice compuesto:

```sql
CREATE INDEX idx_cliente_estado
ON Pedido
(
    IdCliente,
    Estado
);
```

resulta mucho más útil que dos índices independientes en muchas situaciones.

No obstante, el orden de las columnas debe analizarse cuidadosamente.

## Escribir consultas que permitan utilizar índices

El índice puede existir y, aun así, no ser utilizado.

Ejemplo poco recomendable:

```sql
SELECT *
FROM Pedido
WHERE YEAR(FechaPedido) = 2026;
```

Alternativa:

```sql
SELECT *
FROM Pedido
WHERE FechaPedido >= '2026-01-01'
AND FechaPedido < '2027-01-01';
```

La segunda consulta permite al optimizador utilizar el índice sobre `FechaPedido`.

## Verificar el uso mediante EXPLAIN

Nunca debemos asumir que un índice está siendo utilizado.

Es recomendable comprobarlo.

```sql
EXPLAIN
SELECT *
FROM Cliente
WHERE Email = 'ana@empresa.com';
```

Si la columna:

```text
key
```

muestra el índice esperado, sabremos que el optimizador ha decidido emplearlo.

## Revisar periódicamente los índices

Con el paso del tiempo cambian:

- Las consultas.
- Los informes.
- Las funcionalidades.
- El volumen de datos.

Un índice muy útil hace dos años puede haber dejado de aportar valor.

También pueden aparecer índices duplicados o innecesarios.

Por ello conviene revisar periódicamente la estrategia de indexación.

## Evitar crear índices "por si acaso"

Una práctica poco recomendable consiste en añadir índices sobre columnas que quizá puedan utilizarse algún día.

Cada índice implica:

- Espacio adicional.
- Mayor tiempo de inserción.
- Mayor tiempo de actualización.
- Mayor tiempo de eliminación.

Los índices deben responder a necesidades reales.

## Buenas prácticas

- Diseñar índices a partir de las consultas más frecuentes.
- Aprovechar los índices creados por claves primarias y restricciones `UNIQUE`.
- Revisar periódicamente la utilidad de cada índice.
- Comprobar siempre su utilización mediante `EXPLAIN`.
- Evitar índices innecesarios o duplicados.

## Conclusiones

El verdadero valor de un índice depende de cómo se utilice. Un buen diseño requiere comprender tanto la estructura de la base de datos como las consultas ejecutadas por la aplicación. Analizar el comportamiento real mediante `EXPLAIN` permite verificar que los índices están aportando el beneficio esperado.

## Ideas clave

- Los índices deben diseñarse pensando en las consultas.
- No todos los índices aportan mejoras.
- Las claves primarias ya generan índices.
- El optimizador decide cuándo utilizar cada índice.
- Revisar periódicamente la estrategia de indexación es una buena práctica.

