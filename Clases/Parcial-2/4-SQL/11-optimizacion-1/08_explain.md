# EXPLAIN

## Introducción

Hasta ahora hemos aprendido qué son los índices, cómo funcionan internamente y cuándo conviene utilizarlos.

Sin embargo, todavía existe una pregunta fundamental:

> ¿Cómo podemos saber si MySQL está utilizando realmente un índice?

Muchos desarrolladores crean un índice y asumen que automáticamente todas las consultas serán más rápidas.

En realidad, esto no siempre ocurre.

MySQL dispone de un componente denominado **optimizador de consultas** que decide cuál es la mejor estrategia para ejecutar cada sentencia SQL. En ocasiones utilizará un índice y, en otras, decidirá recorrer toda la tabla porque considera que esa opción es más eficiente.

Para conocer las decisiones del optimizador utilizamos la instrucción **EXPLAIN**.

EXPLAIN no ejecuta la consulta para obtener los datos. Su función consiste en mostrar el **plan de ejecución** que MySQL tiene previsto seguir.

Es una de las herramientas más importantes para cualquier administrador de bases de datos y para cualquier desarrollador que desee optimizar consultas.

## ¿Qué es un plan de ejecución?

Un plan de ejecución es una descripción detallada de cómo MySQL pretende resolver una consulta.

Por ejemplo, para una consulta sencilla:

```sql
SELECT *
FROM Cliente
WHERE IdCliente = 250;
```

El plan responderá preguntas como:

- ¿Qué tabla se leerá?
- ¿Qué índice se utilizará?
- ¿Cuántas filas estima MySQL que deberá examinar?
- ¿Será necesario ordenar los datos?
- ¿Se realizará un escaneo completo de la tabla?

Toda esta información resulta esencial para comprender el rendimiento de una consulta.

## Sintaxis básica

La sintaxis es muy sencilla.

Basta con anteponer la palabra:

```sql
EXPLAIN
```

a cualquier consulta.

Por ejemplo:

```sql
EXPLAIN
SELECT *
FROM Cliente
WHERE IdCliente = 250;
```

En lugar de devolver los datos del cliente, MySQL mostrará información sobre la estrategia de ejecución.

## Primer ejemplo

Supongamos la siguiente tabla.

```sql
CREATE TABLE Cliente
(
    IdCliente INT PRIMARY KEY,
    Nombre VARCHAR(100),
    Ciudad VARCHAR(100)
);
```

Consulta.

```sql
EXPLAIN
SELECT *
FROM Cliente
WHERE IdCliente = 15;
```

Un resultado simplificado podría ser:

| id | table | type | key | rows |
|----|-------|------|-----|-----:|
| 1 | Cliente | const | PRIMARY | 1 |

Aunque todavía no comprendamos todas las columnas, ya podemos observar un dato importante.

La columna:

```text
key
```

indica que MySQL utilizará el índice de la clave primaria.

## Segundo ejemplo

Ahora realizamos otra consulta.

```sql
EXPLAIN
SELECT *
FROM Cliente
WHERE Ciudad = 'Bilbao';
```

Supongamos que la columna `Ciudad` no posee índice.

El resultado podría ser:

| id | table | type | key | rows |
|----|-------|------|-----|-----:|
| 1 | Cliente | ALL | NULL | 1200000 |

Este plan nos indica que probablemente MySQL recorrerá toda la tabla.

La diferencia respecto al ejemplo anterior es enorme.

## EXPLAIN no modifica datos

Una característica importante es que EXPLAIN no altera la base de datos.

Podemos utilizarlo con consultas complejas sin preocuparnos por modificar registros.

Incluso puede utilizarse con consultas que incluyen:

- JOIN.
- Subconsultas.
- GROUP BY.
- ORDER BY.
- Funciones.
- Vistas.

Su objetivo siempre será mostrar el plan previsto por el optimizador.

## EXPLAIN y consultas JOIN

Supongamos:

```sql
EXPLAIN
SELECT
    c.Nombre,
    p.FechaPedido
FROM Cliente c
JOIN Pedido p
ON c.IdCliente = p.IdCliente;
```

El resultado contendrá una fila por cada tabla implicada.

De esta forma podremos observar:

- En qué orden se procesan las tablas.
- Qué índices utiliza cada una.
- Qué método de acceso emplea.

Esta información resulta especialmente útil cuando una consulta combina muchas tablas.

## EXPLAIN FORMAT=JSON

Las versiones modernas de MySQL ofrecen una representación mucho más detallada.

```sql
EXPLAIN FORMAT=JSON
SELECT *
FROM Producto
WHERE Categoria = 'Portátiles';
```

El resultado aparece en formato JSON.

Aunque inicialmente pueda parecer más complejo, proporciona mucha más información sobre las decisiones del optimizador.

En esta asignatura trabajaremos principalmente con el formato tabular clásico por resultar más sencillo para comenzar.

## ¿Significa que siempre tiene razón?

No necesariamente.

EXPLAIN muestra la estrategia elegida por el optimizador.

Sin embargo, el optimizador trabaja utilizando estadísticas y estimaciones.

En ocasiones puede seleccionar un plan que no sea el óptimo.

Precisamente por eso resulta tan importante aprender a interpretar sus decisiones.

## Cuándo utilizar EXPLAIN

Es recomendable utilizar EXPLAIN siempre que:

- Una consulta tarde demasiado.
- Se cree un nuevo índice.
- Se elimine un índice.
- Se modifique una consulta compleja.
- Se diseñe una nueva funcionalidad importante.

En proyectos profesionales es habitual analizar con EXPLAIN todas las consultas críticas antes de poner una aplicación en producción.

## Buenas prácticas

- Utilizar EXPLAIN antes de intentar optimizar una consulta.
- Comparar el plan antes y después de crear un índice.
- No asumir que un índice será utilizado automáticamente.
- Analizar especialmente las consultas que procesan grandes volúmenes de datos.
- Familiarizarse con la información proporcionada por el plan de ejecución.

## Conclusiones

EXPLAIN es la herramienta fundamental para comprender cómo ejecuta MySQL una consulta. Gracias a ella es posible descubrir si el optimizador utiliza índices, cuántas filas estima procesar y qué estrategia seguirá para obtener el resultado. Toda optimización seria debe comenzar estudiando el plan de ejecución.

## Ideas clave

- EXPLAIN muestra el plan de ejecución de una consulta.
- No ejecuta la consulta para devolver datos.
- Permite comprobar si un índice está siendo utilizado.
- Ayuda a detectar escaneos completos de tabla.
- Es una herramienta imprescindible para optimizar consultas.
  

