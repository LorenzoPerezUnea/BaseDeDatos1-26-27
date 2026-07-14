# ¿Por qué dos consultas pueden dar el mismo resultado?

## Introducción

Cuando un estudiante comienza a aprender SQL suele preocuparse únicamente por obtener el resultado correcto.

Por ejemplo, si el ejercicio consiste en obtener todos los pedidos pendientes, cualquier consulta que devuelva exactamente esos registros parece válida.

Sin embargo, en el desarrollo profesional esta forma de pensar resulta insuficiente.

Dos consultas pueden producir exactamente el mismo resultado y, aun así, presentar diferencias enormes en cuanto a:

- Tiempo de ejecución.
- Uso de memoria.
- Cantidad de datos leídos.
- Aprovechamiento de índices.
- Facilidad de mantenimiento.
- Claridad del código.

La optimización no consiste únicamente en obtener el resultado correcto, sino en hacerlo de la forma más eficiente posible.

## Equivalencia funcional

Decimos que dos consultas son funcionalmente equivalentes cuando devuelven exactamente el mismo conjunto de resultados.

Por ejemplo, ambas consultas siguientes obtienen los clientes de Madrid.

Primera opción.

```sql
SELECT *
FROM Cliente
WHERE Ciudad = 'Madrid';
```

Segunda opción.

```sql
SELECT *
FROM Cliente
WHERE 'Madrid' = Ciudad;
```

Desde el punto de vista lógico ambas expresiones son equivalentes.

Sin embargo, una puede resultar mucho más legible que la otra.

En este caso la primera opción sigue el estilo habitual utilizado por la mayoría de los desarrolladores.

## Diferencias de rendimiento

Consideremos ahora otro ejemplo.

Consulta A.

```sql
SELECT
    Nombre,
    Precio
FROM Producto;
```

Consulta B.

```sql
SELECT *
FROM Producto;
```

Si la tabla contiene veinte columnas pero la aplicación únicamente necesita dos, ambas consultas producen un resultado funcionalmente útil para el programa.

Sin embargo, la segunda recupera una cantidad mucho mayor de información.

Esto implica:

- Más datos transferidos.
- Mayor uso de memoria.
- Más tiempo de lectura.
- Mayor tráfico por la red.

Una pequeña diferencia en la consulta puede traducirse en una mejora apreciable cuando la tabla contiene millones de registros.

## Un ejemplo con subconsultas

Supongamos que deseamos obtener los clientes que han realizado algún pedido.

Primera opción.

```sql
SELECT *
FROM Cliente
WHERE IdCliente IN
(
    SELECT IdCliente
    FROM Pedido
);
```

Segunda opción.

```sql
SELECT DISTINCT
    c.*
FROM Cliente c
JOIN Pedido p
ON c.IdCliente = p.IdCliente;
```

Dependiendo del volumen de datos, de los índices disponibles y de las decisiones del optimizador, una de las dos estrategias puede resultar claramente superior.

Aunque ambas devuelvan la misma información, el trabajo realizado por MySQL puede ser muy diferente.

## La importancia de la legibilidad

No todas las mejoras están relacionadas con el rendimiento.

Supongamos la siguiente consulta.

```sql
SELECT
A.Nombre,
B.FechaPedido,
C.Nombre
FROM Cliente A
JOIN Pedido B
ON A.IdCliente=B.IdCliente
JOIN Empleado C
ON B.IdEmpleado=C.IdEmpleado;
```

Funciona correctamente.

Sin embargo, el uso de alias poco descriptivos dificulta enormemente su lectura.

Una alternativa más clara sería:

```sql
SELECT
    cli.Nombre,
    ped.FechaPedido,
    emp.Nombre
FROM Cliente AS cli
JOIN Pedido AS ped
    ON cli.IdCliente = ped.IdCliente
JOIN Empleado AS emp
    ON ped.IdEmpleado = emp.IdEmpleado;
```

Ambas consultas producen exactamente el mismo resultado.

La segunda será mucho más sencilla de mantener en el futuro.

## El coste del mantenimiento

En proyectos empresariales una consulta suele modificarse muchas veces a lo largo de su vida útil.

Es posible que:

- Se añadan nuevas columnas.
- Cambien los requisitos.
- Aparezcan nuevos filtros.
- Se incorporen nuevas tablas.

Una consulta clara y bien estructurada facilita enormemente estas modificaciones.

Por el contrario, una consulta difícil de leer aumenta el riesgo de introducir errores.

## El optimizador también influye

MySQL analiza cada consulta y genera un plan de ejecución.

Aunque el optimizador es capaz de transformar muchas expresiones equivalentes, no siempre obtiene exactamente el mismo plan.

Por ejemplo, dos consultas aparentemente similares pueden dar lugar a:

- Distinto orden de los JOIN.
- Uso de índices diferentes.
- Distintas estimaciones de coste.
- Diferente número de registros procesados.

Por ello resulta recomendable comprobar siempre el comportamiento real mediante `EXPLAIN`.

## Pensar como un profesional

Cuando un desarrollador con experiencia escribe una consulta no se limita a preguntarse:

> ¿Funciona?

También analiza cuestiones como:

- ¿Es fácil de comprender?
- ¿Puede aprovechar los índices?
- ¿Escalará correctamente cuando existan millones de registros?
- ¿Podrá otro desarrollador modificarla dentro de cinco años?
- ¿Existe una forma más sencilla de expresar la misma idea?

Este cambio de mentalidad constituye uno de los pasos más importantes en la evolución de un programador.

## Buenas prácticas

- No conformarse con obtener el resultado correcto.
- Comparar distintas formas de resolver un mismo problema.
- Favorecer la claridad del código.
- Medir el rendimiento cuando existan varias alternativas.
- Utilizar `EXPLAIN` para verificar las decisiones del optimizador.

## Conclusiones

Dos consultas SQL pueden ser completamente equivalentes desde el punto de vista funcional y, sin embargo, diferir enormemente en claridad, mantenibilidad y rendimiento. El desarrollo profesional exige analizar todas estas dimensiones antes de decidir qué solución utilizar.

## Ideas clave

- Obtener el resultado correcto es solo el primer objetivo.
- Existen múltiples formas de expresar una misma consulta.
- La claridad del código también forma parte de la calidad.
- El optimizador puede generar planes distintos para consultas equivalentes.
- Las decisiones deben apoyarse en mediciones y no únicamente en la intuición.

