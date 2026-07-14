# Vistas de consulta

## Introducción

El uso más habitual de las vistas consiste en ​**simplificar consultas complejas**​.

En lugar de escribir una consulta larga con múltiples `JOIN`, filtros y cálculos cada vez que la necesitamos, podemos encapsular toda esa lógica dentro de una vista.

A este tipo de vistas las denominaremos ​**vistas de consulta**​.

Son las más frecuentes en aplicaciones empresariales.

---

## Un problema habitual

Supongamos que nuestro departamento comercial consulta constantemente las ventas realizadas.

La información se encuentra repartida entre varias tablas:

* Cliente
* Pedido
* DetallePedido
* Producto

Cada informe requiere combinar todas ellas.

La consulta puede ser extensa y difícil de mantener.

---

## Crear la vista

```sql
CREATE VIEW VistaVentas AS
SELECT
    p.IdPedido,
    p.Fecha,
    c.Nombre AS Cliente,
    pr.Nombre AS Producto,
    dp.Cantidad,
    dp.PrecioUnitario,
    dp.Cantidad * dp.PrecioUnitario AS Importe
FROM Pedido p
INNER JOIN Cliente c
    ON p.IdCliente = c.IdCliente
INNER JOIN DetallePedido dp
    ON p.IdPedido = dp.IdPedido
INNER JOIN Producto pr
    ON dp.IdProducto = pr.IdProducto;
```

Aunque la consulta es relativamente larga, solo tendremos que escribirla una vez.

---

## Utilizar la vista

Ahora consultar las ventas resulta mucho más sencillo.

```sql
SELECT *
FROM VistaVentas;
```

También podemos aplicar filtros:

```sql
SELECT *
FROM VistaVentas
WHERE Importe > 1000;
```

O realizar ordenaciones:

```sql
SELECT *
FROM VistaVentas
ORDER BY Fecha DESC;
```

La vista puede utilizarse exactamente igual que una tabla.

---

## Combinar vistas con otras tablas

Las vistas también pueden participar en nuevas consultas.

Por ejemplo:

```sql
SELECT
    v.Cliente,
    e.Nombre AS Comercial
FROM VistaVentas v
INNER JOIN Empleado e
    ON v.IdPedido = e.IdEmpleado;
```

Aunque la vista ya contiene varios `JOIN`, podemos seguir utilizándola como origen de datos para consultas aún más complejas.

---

## Ventajas

Las vistas de consulta ofrecen numerosos beneficios:

* reducen la longitud de las consultas;
* evitan repetir código SQL;
* facilitan el mantenimiento;
* mejoran la legibilidad;
* permiten reutilizar la misma lógica en múltiples informes.

En proyectos grandes es habitual encontrar decenas o incluso cientos de vistas de este tipo.

---

## Un ejemplo de reutilización

Sin vista:

```sql
SELECT ...
FROM Cliente
JOIN Pedido
JOIN DetallePedido
JOIN Producto;
```

Con vista:

```sql
SELECT *
FROM VistaVentas;
```

La diferencia en claridad y facilidad de mantenimiento es evidente.

---

## Ideas clave

* Las vistas de consulta encapsulan consultas complejas.
* Permiten reutilizar la misma lógica en distintos informes.
* Pueden filtrarse, ordenarse y combinarse como cualquier tabla.
* Son uno de los usos más habituales de las vistas en aplicaciones empresariales.
* Reducen considerablemente la cantidad de código SQL repetido.

