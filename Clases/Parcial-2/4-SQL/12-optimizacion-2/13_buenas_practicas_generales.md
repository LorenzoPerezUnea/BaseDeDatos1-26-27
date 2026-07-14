# Buenas prácticas generales

## Introducción

A lo largo de las dos últimas clases hemos estudiado numerosas técnicas relacionadas con la optimización del rendimiento.

Algunas se centran en el funcionamiento interno de MySQL.

Otras están relacionadas con la escritura del código SQL.

Aunque cada técnica tiene sus particularidades, todas comparten un mismo objetivo:

**construir aplicaciones rápidas, escalables y fáciles de mantener.**

En este capítulo reuniremos las recomendaciones más importantes vistas hasta ahora, organizándolas como una guía práctica para el desarrollo profesional.

## Escribir consultas claras

La primera optimización consiste en escribir consultas fáciles de comprender.

Un código claro:

- Reduce errores.
- Facilita el mantenimiento.
- Permite detectar antes posibles problemas de rendimiento.

Debe mantenerse una estructura uniforme.

```sql
SELECT
    Nombre,
    Precio
FROM Producto
WHERE Stock > 0
ORDER BY Nombre;
```

## Recuperar únicamente la información necesaria

Evite utilizar:

```sql
SELECT *
```

cuando la aplicación solo necesita unas pocas columnas.

Es preferible:

```sql
SELECT
    Nombre,
    Precio
FROM Producto;
```

Esto reduce:

- Lecturas.
- Memoria utilizada.
- Tráfico de red.

## Crear índices con criterio

Los índices deben responder al comportamiento real de la aplicación.

Antes de crear uno conviene preguntarse:

- ¿Qué consultas se ejecutan con mayor frecuencia?
- ¿Qué columnas aparecen en `WHERE`?
- ¿Qué relaciones utilizan `JOIN`?
- ¿Qué consultas realizan ordenaciones frecuentes?

No deben añadirse índices simplemente "por si acaso".

## Comprobar siempre con EXPLAIN

Nunca debemos asumir que una consulta está optimizada.

Es recomendable analizar regularmente:

```sql
EXPLAIN
SELECT ...
```

El plan de ejecución permite conocer:

- Índices utilizados.
- Número estimado de filas.
- Estrategias del optimizador.
- Posibles operaciones costosas.

## Evitar funciones sobre columnas indexadas

Consulta poco recomendable.

```sql
WHERE YEAR(FechaPedido) = 2026
```

Consulta preferible.

```sql
WHERE FechaPedido >= '2026-01-01'
AND FechaPedido < '2027-01-01'
```

Este pequeño cambio puede permitir utilizar un índice existente.

## Mantener una nomenclatura uniforme

Tablas, columnas, índices y alias deben seguir convenciones claras.

Por ejemplo:

```text
Cliente

Pedido

DetallePedido

IdCliente

idx_cliente_email

fk_pedido_cliente
```

La consistencia mejora el mantenimiento del proyecto.

## Optimizar solo cuando sea necesario

No toda consulta necesita optimización.

Si una consulta:

- Es fácil de comprender.
- Se ejecuta pocas veces.
- Presenta un rendimiento adecuado.

puede no ser rentable dedicar tiempo a optimizarla.

Los esfuerzos deben centrarse en los verdaderos cuellos de botella.

## Medir antes y después

Toda optimización debe validarse mediante datos objetivos.

Conviene registrar:

- Tiempo de ejecución.
- Número de filas procesadas.
- Índices utilizados.
- Consumo de recursos.

Optimizar sin medir conduce con frecuencia a conclusiones erróneas.

## Pensar en el mantenimiento

Una consulta extremadamente compleja que ahorra unas pocas décimas de segundo puede no compensar si resulta casi imposible de mantener.

La calidad del software depende del equilibrio entre:

- Rendimiento.
- Claridad.
- Flexibilidad.
- Facilidad de evolución.

## Lista de comprobación

Antes de considerar terminada una consulta conviene revisar los siguientes aspectos:

- ¿Selecciona únicamente las columnas necesarias?
- ¿Utiliza índices adecuados?
- ¿Evita funciones innecesarias?
- ¿Es fácil de leer?
- ¿Se ha comprobado con `EXPLAIN`?
- ¿Puede comprenderla otro desarrollador?
- ¿Está preparada para crecer con el tiempo?

Responder afirmativamente a estas preguntas suele indicar que la consulta presenta una buena calidad técnica.

## Buenas prácticas

- Escribir primero una solución correcta.
- Optimizar únicamente cuando sea necesario.
- Mantener un estilo uniforme.
- Revisar periódicamente las consultas más utilizadas.
- Basar todas las decisiones en mediciones objetivas.
- Priorizar siempre la claridad sin descuidar el rendimiento.

## Conclusiones

La optimización no consiste en aplicar trucos aislados, sino en desarrollar un método de trabajo basado en consultas bien diseñadas, índices adecuados, análisis del plan de ejecución y una mejora continua del código. Estas buenas prácticas permiten construir aplicaciones robustas capaces de mantener un alto rendimiento incluso cuando el volumen de datos crece de forma considerable.

## Ideas clave

- La calidad del código influye directamente en el rendimiento.
- Los índices deben diseñarse según el uso real de la aplicación.
- `EXPLAIN` es una herramienta imprescindible.
- Optimizar requiere medir.
- El mejor código es aquel que combina eficiencia, claridad y facilidad de mantenimiento.

