# Lectura del plan de ejecución

## Introducción

En el apartado anterior aprendimos a utilizar la instrucción `EXPLAIN`.

Ahora debemos aprender a interpretar la información que devuelve.

La primera vez que un estudiante ejecuta EXPLAIN suele encontrarse con una tabla llena de columnas desconocidas.

Por ejemplo:

| id | select_type | table | type | possible_keys | key | key_len | ref | rows | filtered | Extra |
|----|-------------|-------|------|---------------|-----|---------|-----|-----:|---------:|-------|

A simple vista puede parecer información difícil de comprender.

Sin embargo, unas pocas columnas proporcionan casi toda la información necesaria para detectar la mayoría de los problemas de rendimiento.

En este apartado estudiaremos las más importantes.

## Un ejemplo

Consulta.

```sql
EXPLAIN
SELECT *
FROM Cliente
WHERE IdCliente = 120;
```

Resultado simplificado.

| id | table | type | key | rows | Extra |
|----|-------|------|-----|-----:|-------|
| 1 | Cliente | const | PRIMARY | 1 | |

Este plan nos indica que MySQL accederá directamente al registro utilizando la clave primaria.

Es una consulta extremadamente eficiente.

## Columna `table`

La columna:

```text
table
```

indica qué tabla está procesando MySQL.

En consultas sencillas aparecerá una única tabla.

Por ejemplo.

| table |
|--------|
| Cliente |

En consultas con JOIN aparecerán varias filas.

Cada fila corresponderá a una tabla distinta.

## Columna `type`

Es probablemente una de las columnas más importantes.

Indica el método de acceso que utilizará MySQL.

Algunos valores habituales son:

| type | Significado |
|------|-------------|
| const | Acceso mediante clave primaria o índice único. Muy eficiente. |
| eq_ref | Acceso mediante índice único en un JOIN. |
| ref | Acceso mediante índice no único. |
| range | Lectura de un rango del índice. |
| index | Recorrido completo del índice. |
| ALL | Escaneo completo de la tabla. |

En general:

- `const` suele ser excelente.
- `ref` y `range` suelen ser buenos.
- `ALL` merece una revisión, especialmente en tablas grandes.

## Columna `possible_keys`

Indica los índices que podrían utilizarse.

Por ejemplo.

| possible_keys |
|---------------|
| PRIMARY, idx_cliente_ciudad |

Esto no significa que vayan a utilizarse.

Simplemente son candidatos.

El optimizador elegirá uno de ellos, o incluso ninguno.

## Columna `key`

Esta columna muestra el índice finalmente seleccionado.

Ejemplo.

| key |
|-----|
| PRIMARY |

Si aparece:

```text
NULL
```

significa que no se ha utilizado ningún índice.

No siempre es un problema.

En tablas pequeñas puede ser perfectamente normal.

Pero en tablas con millones de registros conviene analizar la situación.

## Columna `rows`

Esta columna indica el número aproximado de filas que MySQL espera examinar.

Por ejemplo.

| rows |
|------:|
| 1 |

Excelente.

Otro ejemplo.

| rows |
|------:|
| 8500000 |

Esto significa que el optimizador estima revisar aproximadamente ocho millones y medio de registros.

No implica necesariamente que vaya a devolver esa cantidad de filas.

Simplemente representa el trabajo estimado.

Cuanto menor sea este número, normalmente mejor será el rendimiento.

## Columna `Extra`

La columna `Extra` contiene información adicional muy útil.

Algunos valores frecuentes son:

### Using where

```text
Using where
```

Significa que MySQL aplica una condición `WHERE` para filtrar registros.

Es completamente normal.

### Using index

```text
Using index
```

Indica que toda la información necesaria puede obtenerse directamente del índice sin acceder a la tabla.

Este comportamiento suele ofrecer un rendimiento excelente.

### Using temporary

```text
Using temporary
```

MySQL necesita crear una tabla temporal para resolver la consulta.

No siempre es un problema, pero puede afectar al rendimiento en consultas complejas.

### Using filesort

```text
Using filesort
```

MySQL necesita realizar una ordenación adicional.

No significa necesariamente que utilice archivos en disco.

El nombre es histórico.

Sin embargo, suele indicar que existe una operación de ordenación que podría optimizarse.

## Interpretando un ejemplo completo

Consulta.

```sql
EXPLAIN
SELECT *
FROM Pedido
WHERE FechaPedido >= '2026-01-01';
```

Resultado.

| table | type | key | rows | Extra |
|--------|------|-----|------:|-------|
| Pedido | range | idx_fecha | 1850 | Using where |

Interpretación.

- Se utiliza un índice.
- Solo se recorrerá un rango del índice.
- Se estima revisar unas 1850 filas.
- Posteriormente se aplicará el filtro `WHERE`.

Este plan suele considerarse eficiente.

## Señales de alerta

Conviene revisar cuidadosamente consultas cuyo plan muestre:

- `ALL` sobre tablas muy grandes.
- `rows` extremadamente elevado.
- `key = NULL` cuando debería existir un índice.
- Uso frecuente de tablas temporales.
- Ordenaciones innecesarias.

Estas situaciones no implican automáticamente un problema, pero suelen ser buenos puntos de partida para comenzar una optimización.

## Buenas prácticas

- Leer siempre el plan completo antes de modificar una consulta.
- Prestar especial atención a las columnas `type`, `key` y `rows`.
- Comparar los planes antes y después de crear un índice.
- No optimizar únicamente por intuición; utilizar siempre datos objetivos.
- Recordar que EXPLAIN muestra estimaciones, no tiempos reales.

## Conclusiones

Interpretar correctamente un plan de ejecución permite comprender las decisiones tomadas por el optimizador de MySQL. Analizando columnas como `type`, `key` y `rows` es posible detectar rápidamente consultas ineficientes y decidir qué cambios pueden mejorar su rendimiento.

## Ideas clave

- El plan de ejecución describe cómo MySQL resolverá una consulta.
- `type` indica el método de acceso utilizado.
- `key` muestra el índice finalmente seleccionado.
- `rows` estima el trabajo que realizará el motor.
- La columna `Extra` proporciona información muy útil para detectar posibles optimizaciones.

