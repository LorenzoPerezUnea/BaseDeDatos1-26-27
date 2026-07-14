# Buenas prácticas

## Introducción

A lo largo de esta clase hemos estudiado cómo trabaja MySQL internamente cuando ejecuta una consulta, cómo funcionan los índices y de qué manera podemos analizar un plan de ejecución mediante `EXPLAIN`.

Todos estos conocimientos permiten optimizar bases de datos de forma profesional. Sin embargo, conocer las herramientas no garantiza obtener buenos resultados.

La diferencia entre un desarrollador con experiencia y otro que comienza suele encontrarse en los hábitos de trabajo.

Las buenas prácticas ayudan a diseñar bases de datos que continúan ofreciendo un buen rendimiento incluso cuando el volumen de información crece de forma considerable.

Este documento recopila las recomendaciones más importantes relacionadas con la optimización mediante índices y el análisis de consultas.

## Diseñar pensando en las consultas

Uno de los errores más habituales consiste en diseñar una base de datos pensando únicamente en almacenar información.

Una base de datos no existe únicamente para guardar datos.

Su función principal es recuperarlos de forma eficiente.

Antes de crear un índice conviene preguntarse:

- ¿Qué consultas realizará la aplicación?
- ¿Qué columnas aparecen con mayor frecuencia en `WHERE`?
- ¿Qué tablas participan en los `JOIN`?
- ¿Qué columnas se utilizan para ordenar resultados?
- ¿Qué informes se ejecutarán diariamente?

Los índices deben responder a necesidades reales de acceso a la información.

## Analizar antes de optimizar

Nunca debe comenzarse una optimización modificando consultas al azar.

El proceso correcto consiste en:

1. Detectar una consulta lenta.
2. Medir su rendimiento.
3. Analizar el plan mediante `EXPLAIN`.
4. Identificar el problema.
5. Aplicar una mejora.
6. Volver a medir.

De esta forma cada cambio queda justificado mediante datos objetivos.

## Crear únicamente los índices necesarios

Cada índice aporta ventajas durante las consultas, pero también introduce costes.

Antes de añadir uno nuevo conviene comprobar:

- Si ya existe otro índice equivalente.
- Si realmente mejora las consultas.
- Si compensa el coste de mantenimiento.

Una tabla con demasiados índices puede ofrecer un excelente rendimiento en lectura y un comportamiento muy pobre durante las inserciones y actualizaciones.

## Aprovechar los índices existentes

Las claves primarias generan automáticamente un índice.

Las restricciones `UNIQUE` también suelen crear uno.

Antes de diseñar nuevos índices conviene revisar los ya existentes.

Muchas veces un índice adicional resulta completamente innecesario.

## Elegir correctamente el orden en índices compuestos

Cuando un índice contiene varias columnas, el orden es fundamental.

Por ejemplo:

```sql
CREATE INDEX idx_pedido_cliente_fecha
ON Pedido
(
    IdCliente,
    FechaPedido
);
```

Este índice está optimizado para consultas que comienzan filtrando por `IdCliente`.

Si la mayoría de las consultas filtran primero por la fecha, probablemente el orden adecuado sea el contrario.

La decisión debe basarse en el uso real de la aplicación.

## Evitar funciones sobre columnas indexadas

Siempre que sea posible, las condiciones deben escribirse de forma que el optimizador pueda utilizar el índice.

Menos recomendable:

```sql
WHERE YEAR(FechaPedido) = 2026;
```

Preferible:

```sql
WHERE FechaPedido >= '2026-01-01'
AND FechaPedido < '2027-01-01';
```

La segunda versión permite aprovechar el índice de forma mucho más eficiente.

## Solicitar únicamente la información necesaria

Es recomendable evitar:

```sql
SELECT *
```

cuando no sea imprescindible.

Seleccionar únicamente las columnas necesarias:

- Reduce el tráfico por la red.
- Disminuye el uso de memoria.
- Puede permitir el uso de índices de cobertura.
- Mejora la velocidad de respuesta.

## Revisar periódicamente los índices

Las aplicaciones evolucionan.

Las consultas también.

Un índice que resultaba muy útil hace un año puede haber dejado de utilizarse.

Es recomendable revisar periódicamente:

- Índices duplicados.
- Índices nunca utilizados.
- Índices sobre columnas que ya no aparecen en consultas.

Eliminar estructuras innecesarias simplifica el mantenimiento y mejora el rendimiento de las operaciones de escritura.

## No optimizar prematuramente

No todas las consultas necesitan ser optimizadas.

Una consulta que se ejecuta una vez al mes difícilmente justificará la creación de varios índices adicionales.

Conviene centrar los esfuerzos en:

- Consultas frecuentes.
- Procesos críticos.
- Informes diarios.
- Operaciones que afectan directamente a los usuarios.

## Documentar las decisiones

Cuando se crea un índice importante resulta recomendable documentar:

- Qué problema resuelve.
- Qué consultas pretende acelerar.
- Cuándo fue creado.
- Quién tomó la decisión.

Esta información facilita enormemente el mantenimiento futuro de la base de datos.

## Lista de comprobación

Antes de dar por optimizada una consulta conviene verificar:

- ¿Existe un índice adecuado?
- ¿Lo utiliza realmente MySQL?
- ¿Ha disminuido el número de filas examinadas?
- ¿Se mantiene el mismo resultado?
- ¿Ha mejorado el tiempo de respuesta?
- ¿El coste adicional del índice está justificado?

Responder afirmativamente a todas estas preguntas suele indicar que la optimización ha sido correcta.

## Conclusiones

La optimización no consiste en aplicar técnicas aisladas, sino en seguir un proceso ordenado de análisis, medición y mejora. Las buenas prácticas permiten construir bases de datos que mantienen un rendimiento elevado incluso cuando aumentan el volumen de información y el número de usuarios concurrentes.

## Ideas clave

- Diseñar índices pensando en las consultas reales.
- Medir antes y después de optimizar.
- Evitar índices innecesarios.
- Revisar periódicamente las estructuras existentes.
- Documentar las decisiones de optimización.

