# Caso práctico: Empresa

## Introducción

Para finalizar la parte práctica de la clase construiremos varias vistas sobre la base de datos de la empresa que hemos venido desarrollando durante el curso.

Nuestro objetivo será comprobar cómo una única consulta puede reutilizarse en diferentes situaciones.

---

# Vista 1. Productos disponibles

Creamos una vista con la información más relevante del catálogo.

```sql
CREATE VIEW VistaProductosDisponibles AS
SELECT
    IdProducto,
    Nombre,
    Precio,
    Stock
FROM Producto
WHERE Stock > 0;
```

Consultamos la vista:

```sql
SELECT *
FROM VistaProductosDisponibles;
```

Ahora cualquier aplicación podrá acceder únicamente a los productos disponibles.

---

# Vista 2. Pedidos con nombre del cliente

En lugar de realizar un `JOIN` continuamente:

```sql
CREATE VIEW VistaPedidosClientes AS
SELECT
    p.IdPedido,
    p.Fecha,
    p.Total,
    c.Nombre AS Cliente
FROM Pedido p
INNER JOIN Cliente c
ON p.IdCliente = c.IdCliente;
```

Consulta:

```sql
SELECT *
FROM VistaPedidosClientes;
```

---

# Vista 3. Resumen de ventas

Creamos una vista para obtener el importe total vendido por cliente.

```sql
CREATE VIEW VistaVentasClientes AS
SELECT
    c.IdCliente,
    c.Nombre,
    SUM(p.Total) AS TotalComprado
FROM Cliente c
INNER JOIN Pedido p
ON c.IdCliente = p.IdCliente
GROUP BY
    c.IdCliente,
    c.Nombre;
```

Consulta:

```sql
SELECT *
FROM VistaVentasClientes
ORDER BY TotalComprado DESC;
```

Esta vista resulta muy útil para elaborar informes comerciales.

---

# Vista 4. Catálogo para clientes

Supongamos que no queremos mostrar el coste interno del producto.

Creamos una vista pública.

```sql
CREATE VIEW VistaCatalogoPublico AS
SELECT
    Nombre,
    Precio
FROM Producto;
```

La aplicación web consultará:

```sql
SELECT *
FROM VistaCatalogoPublico;
```

De este modo no tendrá acceso a otras columnas de la tabla.

---

# Vista 5. Clientes activos

Mostramos únicamente los clientes que ya han realizado pedidos.

```sql
CREATE VIEW VistaClientesActivos AS
SELECT DISTINCT
    c.IdCliente,
    c.Nombre
FROM Cliente c
INNER JOIN Pedido p
ON c.IdCliente = p.IdCliente;
```

Consulta:

```sql
SELECT *
FROM VistaClientesActivos;
```

---

## Ejercicio propuesto

Crear una vista denominada:

```text
VistaEmpleadosVentas
```

que muestre:

* nombre del empleado;
* cargo;
* número de pedidos gestionados.

Una vez creada:

1. Consultarla.
2. Ordenarla por número de pedidos.
3. Mostrar únicamente los empleados con más de 20 pedidos.

Este ejercicio obligará al estudiante a combinar:

* `JOIN`;
* `GROUP BY`;
* funciones de agregación;
* vistas.

---

## Conclusión

Este caso práctico muestra cómo una misma base de datos puede ofrecer diferentes "formas de ver" la información según las necesidades de cada usuario o aplicación.

Las tablas siguen siendo las mismas, pero las vistas proporcionan representaciones especializadas, reutilizables y fáciles de mantener.

---

## Ideas clave

* Una misma base de datos puede contener numerosas vistas especializadas.
* Las vistas simplifican informes y aplicaciones.
* Es habitual crear vistas diferentes para distintos departamentos.
* El código SQL resulta mucho más limpio y reutilizable.
* Las vistas constituyen una capa intermedia muy útil entre las tablas y las aplicaciones.

