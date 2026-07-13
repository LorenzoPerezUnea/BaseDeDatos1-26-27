# Caso práctico: Sistema de gestión empresarial

## Introducción

Para finalizar el estudio de los distintos tipos de `JOIN`, construiremos una consulta similar a las que encontramos en un sistema ERP o de comercio electrónico.

Trabajaremos con las siguientes tablas:

* `Cliente`
* `Pedido`
* `DetallePedido`
* `Producto`
* `Categoria`
* `Empleado`

Nuestro objetivo será generar un informe completo de ventas.

---

## Modelo simplificado

```text
Cliente
    │
    ▼
Pedido
    │
    ▼
DetallePedido
    ├──────────────► Producto ─────────────► Categoria
    │
    └──────────────► Empleado
```

Cada tabla aporta una parte de la información.

---

## Consulta completa

```sql
SELECT
    c.Nombre AS Cliente,
    p.IdPedido,
    p.Fecha,
    e.Nombre AS Empleado,
    pr.Nombre AS Producto,
    ca.Nombre AS Categoria,
    dp.Cantidad,
    pr.Precio,
    dp.Cantidad * pr.Precio AS Importe
FROM Cliente AS c

INNER JOIN Pedido AS p
    ON c.IdCliente = p.IdCliente

INNER JOIN Empleado AS e
    ON p.IdEmpleado = e.IdEmpleado

INNER JOIN DetallePedido AS dp
    ON p.IdPedido = dp.IdPedido

INNER JOIN Producto AS pr
    ON dp.IdProducto = pr.IdProducto

INNER JOIN Categoria AS ca
    ON pr.IdCategoria = ca.IdCategoria

ORDER BY
    p.Fecha,
    c.Nombre;
```

---

## Analizando la consulta

Cada `JOIN` incorpora nueva información al resultado:

| Tabla         | Información aportada      |
| --------------- | ---------------------------- |
| Cliente       | Nombre del cliente         |
| Pedido        | Número y fecha del pedido |
| Empleado      | Comercial responsable      |
| DetallePedido | Cantidad comprada          |
| Producto      | Nombre y precio            |
| Categoría    | Familia del producto       |

Esta es una de las grandes ventajas de las bases de datos relacionales: cada dato se almacena una sola vez, pero puede combinarse dinámicamente durante las consultas.

---

## Resultado esperado

| Cliente | Pedido | Empleado | Producto  | Categoría   | Cantidad | Importe |
| --------- | -------: | ---------- | ----------- | -------------- | ---------: | --------: |
| Ana     |    101 | Laura    | Portátil | Informática |        1 |  950.00 |
| Ana     |    101 | Laura    | Ratón    | Periféricos |        2 |   50.00 |
| Marta   |    102 | Pedro    | Monitor   | Informática |        1 |  320.00 |

Cada fila representa una línea del pedido.

---

## Variación 1: Clientes sin pedidos

Si el departamento comercial desea identificar clientes inactivos:

```sql
SELECT
    c.Nombre
FROM Cliente AS c

LEFT JOIN Pedido AS p
ON c.IdCliente = p.IdCliente

WHERE p.IdPedido IS NULL;
```

Esta consulta resulta muy útil para campañas de fidelización.

---

## Variación 2: Ventas por categoría

```sql
SELECT
    ca.Nombre,
    SUM(dp.Cantidad * pr.Precio) AS TotalVentas
FROM Categoria AS ca

INNER JOIN Producto AS pr
ON ca.IdCategoria = pr.IdCategoria

INNER JOIN DetallePedido AS dp
ON pr.IdProducto = dp.IdProducto

GROUP BY ca.Nombre

ORDER BY TotalVentas DESC;
```

Aquí observamos cómo los `JOIN` pueden combinarse con `GROUP BY` y funciones de agregación para construir informes analíticos.

---

## Conclusiones

Este tipo de consultas representa el trabajo cotidiano de un desarrollador de aplicaciones empresariales.

Los sistemas ERP, CRM, plataformas de comercio electrónico y aplicaciones de gestión ejecutan continuamente consultas similares, muchas de ellas con diez o más tablas relacionadas.

Dominar los `JOIN` significa ser capaz de explotar todo el potencial de una base de datos relacional.

---

## Ideas clave

* Los `JOIN` permiten reconstruir información distribuida entre múltiples tablas.
* Las consultas profesionales suelen combinar numerosos `JOIN`.
* Es habitual mezclar `JOIN`, funciones de agregación, `GROUP BY`, `WHERE` y `ORDER BY`.
* Un buen conocimiento del modelo relacional facilita enormemente la construcción de consultas complejas.
* El dominio de los `JOIN` constituye uno de los pilares fundamentales del desarrollo con SQL.

