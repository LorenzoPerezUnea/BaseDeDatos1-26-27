# Legibilidad del código SQL

## Introducción

Cuando se habla de optimización, muchas personas piensan inmediatamente en índices, memoria, procesadores o discos de alta velocidad.

Sin embargo, una gran parte del rendimiento de un proyecto depende de algo mucho más sencillo: **la calidad del código SQL**.

Una consulta puede ejecutarse rápidamente hoy, pero si dentro de seis meses ningún desarrollador es capaz de comprenderla, mantenerla o modificarla sin introducir errores, esa consulta terminará convirtiéndose en un problema para el proyecto.

La legibilidad consiste en escribir SQL de forma que cualquier desarrollador pueda comprender rápidamente qué hace una consulta y por qué está escrita de esa manera.

En equipos profesionales es habitual que decenas de personas trabajen sobre la misma base de datos durante años. Un código SQL claro reduce el tiempo necesario para localizar errores, incorporar nuevas funcionalidades y optimizar consultas existentes.

## ¿Qué significa que una consulta sea legible?

Una consulta legible es aquella cuya intención puede comprenderse sin necesidad de analizar cada línea durante varios minutos.

Por ejemplo:

```sql
SELECT
    Nombre,
    Precio
FROM Producto
WHERE Stock > 0;
```

Incluso alguien que no conozca la aplicación puede deducir fácilmente que obtiene los productos disponibles.

Comparemos con una versión equivalente:

```sql
SELECT Nombre,Precio FROM Producto WHERE Stock>0;
```

El resultado es exactamente el mismo.

Sin embargo, la primera versión facilita mucho más la lectura.

## Utilizar una indentación consistente

La indentación permite identificar visualmente las distintas partes de una consulta.

Una buena práctica consiste en colocar cada cláusula principal en una línea independiente.

```sql
SELECT
    Nombre,
    Precio,
    Stock
FROM Producto
WHERE Categoria = 'Monitores'
ORDER BY Precio;
```

Cuando las consultas incluyen varias tablas o condiciones, la diferencia resulta aún más evidente.

Consulta difícil de leer:

```sql
SELECT c.Nombre,p.FechaPedido,e.Nombre
FROM Cliente c JOIN Pedido p ON c.IdCliente=p.IdCliente
JOIN Empleado e ON e.IdEmpleado=p.IdEmpleado
WHERE p.Estado='Pendiente';
```

Consulta equivalente con un formato adecuado:

```sql
SELECT
    c.Nombre,
    p.FechaPedido,
    e.Nombre
FROM Cliente AS c
JOIN Pedido AS p
    ON c.IdCliente = p.IdCliente
JOIN Empleado AS e
    ON e.IdEmpleado = p.IdEmpleado
WHERE p.Estado = 'Pendiente';
```

La segunda versión permite identificar rápidamente cada parte de la consulta.

## Colocar una columna por línea

Cuando una consulta devuelve muchas columnas es recomendable escribir cada una en una línea distinta.

En lugar de:

```sql
SELECT Nombre,Precio,Stock,Categoria,Proveedor
FROM Producto;
```

Es preferible:

```sql
SELECT
    Nombre,
    Precio,
    Stock,
    Categoria,
    Proveedor
FROM Producto;
```

Añadir o eliminar columnas resulta mucho más sencillo.

## Alinear cláusulas importantes

Todas las cláusulas principales deberían comenzar en la misma posición.

Por ejemplo:

```sql
SELECT
FROM
WHERE
GROUP BY
HAVING
ORDER BY
LIMIT
```

Esta organización permite localizar rápidamente la estructura general de la consulta.

## Utilizar espacios correctamente

Los espacios mejoran notablemente la legibilidad.

Poco recomendable:

```sql
WHERE Precio>=100
```

Más recomendable:

```sql
WHERE Precio >= 100
```

Lo mismo ocurre con las operaciones aritméticas.

```sql
Precio * Cantidad
```

resulta más fácil de leer que

```sql
Precio*Cantidad
```

## Utilizar mayúsculas para palabras reservadas

No existe una obligación técnica.

Las siguientes consultas funcionan exactamente igual.

```sql
select *
from Cliente;
```

```sql
SELECT *
FROM Cliente;
```

Sin embargo, en proyectos profesionales suele utilizarse la segunda opción porque permite distinguir fácilmente:

- Palabras reservadas del lenguaje.
- Nombres de tablas.
- Nombres de columnas.

## Agrupar condiciones complejas

Cuando existen muchas condiciones es recomendable organizarlas claramente.

Por ejemplo:

```sql
WHERE
    Estado = 'Pendiente'
    AND FechaPedido >= '2026-01-01'
    AND Total > 500;
```

Esta presentación facilita localizar cada condición.

## Comentar cuando sea necesario

No todas las consultas necesitan comentarios.

Sin embargo, cuando una parte del código implementa una regla de negocio compleja puede resultar conveniente añadir una breve explicación.

Ejemplo:

```sql
-- Clientes con compras superiores a 10 000 €
SELECT
    Nombre
FROM Cliente
WHERE TotalCompras > 10000;
```

Los comentarios deben explicar el propósito de la consulta, no describir literalmente lo que ya resulta evidente.

## Evitar consultas excesivamente largas

Una consulta con cientos de líneas suele ser difícil de mantener.

En muchos casos puede dividirse utilizando:

- Vistas.
- Subconsultas bien organizadas.
- Expresiones comunes (CTE), cuando proceda.
- Procedimientos almacenados.

El objetivo consiste en reducir la complejidad sin modificar el resultado.

## Pensar en el siguiente desarrollador

Existe una conocida frase en ingeniería del software:

> "El código se escribe una vez, pero se lee muchas veces."

Esta idea también es válida para SQL.

Cuando escribimos una consulta debemos pensar que probablemente otra persona tendrá que comprenderla dentro de varios años.

Si el código es claro, el mantenimiento será mucho más sencillo.

## Buenas prácticas

- Mantener una indentación uniforme.
- Escribir una columna por línea en consultas extensas.
- Utilizar espacios alrededor de operadores.
- Escribir las palabras reservadas en mayúsculas.
- Organizar claramente las condiciones.
- Evitar consultas innecesariamente largas.
- Añadir comentarios únicamente cuando aporten información útil.

## Conclusiones

La legibilidad no mejora directamente la velocidad de ejecución de una consulta, pero sí mejora enormemente la calidad del proyecto. Un código SQL claro reduce errores, facilita el mantenimiento y permite identificar con mayor rapidez posibles problemas de rendimiento.

## Ideas clave

- La legibilidad forma parte de la calidad del software.
- Una buena indentación facilita comprender las consultas.
- El formato debe ser consistente en todo el proyecto.
- El código SQL se mantiene durante muchos años.
- Escribir para otros desarrolladores es tan importante como escribir para el ordenador.

