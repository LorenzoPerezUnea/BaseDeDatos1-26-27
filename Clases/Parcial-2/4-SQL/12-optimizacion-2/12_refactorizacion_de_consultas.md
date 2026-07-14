# Refactorización de consultas

## Introducción

En ingeniería del software existe un concepto ampliamente conocido denominado **refactorización**.

Consiste en modificar el código para mejorar su calidad interna **sin alterar su comportamiento externo**.

En otras palabras, una vez finalizada la refactorización, el programa debe seguir produciendo exactamente el mismo resultado, pero el código será:

- Más fácil de comprender.
- Más sencillo de mantener.
- Más flexible para futuras modificaciones.
- En muchos casos, también más eficiente.

Este mismo principio puede aplicarse al lenguaje SQL.

Una consulta SQL escrita hace varios años puede seguir funcionando perfectamente y, sin embargo, resultar difícil de leer, contener redundancias o desaprovechar las capacidades del optimizador.

La refactorización busca mejorar esas consultas sin modificar la información que devuelven.

## ¿Cuándo conviene refactorizar una consulta?

No todas las consultas necesitan ser modificadas.

Una buena candidata suele presentar alguna de estas características:

- Código difícil de leer.
- Exceso de subconsultas.
- Alias poco descriptivos.
- Uso innecesario de `SELECT *`.
- Condiciones redundantes.
- Repetición de expresiones.
- Consultas excesivamente largas.
- Problemas detectados mediante `EXPLAIN`.

## Ejemplo 1. Mejorar la legibilidad

Consulta original.

```sql
SELECT c.Nombre,p.FechaPedido,e.Nombre
FROM Cliente c
JOIN Pedido p
ON c.IdCliente=p.IdCliente
JOIN Empleado e
ON e.IdEmpleado=p.IdEmpleado;
```

Consulta refactorizada.

```sql
SELECT
    cli.Nombre,
    ped.FechaPedido,
    emp.Nombre
FROM Cliente AS cli
JOIN Pedido AS ped
    ON cli.IdCliente = ped.IdCliente
JOIN Empleado AS emp
    ON emp.IdEmpleado = ped.IdEmpleado;
```

El resultado es exactamente el mismo.

Sin embargo, la segunda versión facilita mucho más su comprensión.

## Ejemplo 2. Eliminar SELECT *

Consulta original.

```sql
SELECT *
FROM Producto;
```

Consulta refactorizada.

```sql
SELECT
    Nombre,
    Precio,
    Stock
FROM Producto;
```

Ahora únicamente se recupera la información necesaria.

## Ejemplo 3. Simplificar condiciones

Consulta original.

```sql
SELECT *
FROM Pedido
WHERE NOT (Estado <> 'Pendiente');
```

Consulta refactorizada.

```sql
SELECT *
FROM Pedido
WHERE Estado = 'Pendiente';
```

La lógica es mucho más evidente.

## Ejemplo 4. Reescribir funciones sobre columnas indexadas

Consulta original.

```sql
SELECT *
FROM Pedido
WHERE YEAR(FechaPedido) = 2026;
```

Consulta refactorizada.

```sql
SELECT *
FROM Pedido
WHERE FechaPedido >= '2026-01-01'
AND FechaPedido < '2027-01-01';
```

Además de resultar más eficiente, esta versión permite aprovechar un posible índice sobre `FechaPedido`.

## Ejemplo 5. Eliminar redundancias

Consulta original.

```sql
SELECT *
FROM Cliente
WHERE Activo = 1
AND Activo = 1;
```

Consulta refactorizada.

```sql
SELECT *
FROM Cliente
WHERE Activo = 1;
```

Toda condición innecesaria incrementa la complejidad del código.

## Mejorar sin cambiar el comportamiento

La regla más importante de cualquier refactorización es muy sencilla:

> El resultado debe seguir siendo exactamente el mismo.

Antes de dar por finalizado el proceso conviene comprobar:

- Que el número de registros coincide.
- Que los datos devueltos son los mismos.
- Que no se han introducido errores lógicos.

Solo entonces podremos afirmar que la refactorización ha sido correcta.

## Refactorización y rendimiento

Aunque muchas refactorizaciones persiguen mejorar la legibilidad, algunas también producen mejoras de rendimiento.

No obstante, nunca debe darse por supuesto.

Toda modificación debe verificarse mediante:

```sql
EXPLAIN
```

y, siempre que sea posible, midiendo tiempos reales de ejecución.

## Refactorización continua

Las aplicaciones evolucionan constantemente.

Cada nueva funcionalidad añade consultas, filtros y relaciones.

Por ello la refactorización no debe entenderse como una tarea puntual, sino como una práctica habitual del desarrollo profesional.

Pequeñas mejoras realizadas de forma continua evitan que el código termine siendo difícil de mantener.

## Buenas prácticas

- Refactorizar únicamente cuando exista un beneficio claro.
- Mantener siempre el mismo resultado.
- Simplificar expresiones complejas.
- Mejorar la legibilidad antes de añadir nuevas funcionalidades.
- Comprobar el rendimiento antes y después de cada cambio.
- Documentar las modificaciones importantes.

## Conclusiones

La refactorización constituye una herramienta esencial para mantener la calidad del código SQL. Unas consultas bien organizadas facilitan el mantenimiento, reducen errores y permiten optimizar la aplicación de forma progresiva sin modificar su comportamiento funcional.

## Ideas clave

- Refactorizar significa mejorar el código sin cambiar el resultado.
- La claridad facilita el mantenimiento.
- Las mejoras de rendimiento deben medirse.
- Una consulta sencilla suele ser más fácil de optimizar.
- La refactorización debe formar parte del desarrollo habitual.

