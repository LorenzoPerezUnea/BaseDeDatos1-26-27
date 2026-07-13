# Caso práctico completo

## Introducción

En este caso práctico integraremos prácticamente todos los conceptos estudiados en esta clase.

Trabajaremos sobre el siguiente esquema simplificado:

* `Cliente`
* `Pedido`
* `DetallePedido`
* `Producto`
* `Categoria`
* `Empleado`

Nuestro objetivo será construir distintos informes empresariales utilizando subconsultas de diferentes tipos.

No existe una única solución para todos los problemas. En algunos casos utilizaremos subconsultas simples, en otros correlacionadas y, cuando sea conveniente, operadores como `EXISTS`.

---

# Caso 1. Productos con un precio superior a la media

Queremos identificar los productos cuyo precio está por encima del precio medio de todos los productos.

```sql
SELECT
    IdProducto,
    Nombre,
    Precio
FROM Producto
WHERE Precio >
(
    SELECT AVG(Precio)
    FROM Producto
)
ORDER BY Precio DESC;
```

### ¿Qué hace la consulta?

1. Calcula el precio medio de todos los productos.
2. Compara cada producto con ese valor.
3. Devuelve únicamente los productos cuyo precio sea superior.

Este es probablemente el ejemplo más clásico de subconsulta simple.

---

# Caso 2. Clientes que han realizado compras

El departamento comercial quiere obtener únicamente clientes activos.

```sql
SELECT
    c.IdCliente,
    c.Nombre
FROM Cliente c
WHERE EXISTS
(
    SELECT 1
    FROM Pedido p
    WHERE p.IdCliente = c.IdCliente
);
```

Aquí no interesa saber cuántos pedidos tiene cada cliente.

Solo queremos saber si existe al menos uno.

`EXISTS` expresa perfectamente esa intención.

---

# Caso 3. Clientes sin actividad

Ahora buscamos justamente lo contrario.

```sql
SELECT
    c.IdCliente,
    c.Nombre
FROM Cliente c
WHERE NOT EXISTS
(
    SELECT 1
    FROM Pedido p
    WHERE p.IdCliente = c.IdCliente
);
```

Este informe es muy habitual en campañas de fidelización o recuperación de clientes.

---

# Caso 4. Número de pedidos por cliente

Ahora utilizaremos una subconsulta correlacionada.

```sql
SELECT
    c.Nombre,
    (
        SELECT COUNT(*)
        FROM Pedido p
        WHERE p.IdCliente = c.IdCliente
    ) AS TotalPedidos
FROM Cliente c
ORDER BY TotalPedidos DESC;
```

Cada cliente obtiene un valor diferente.

La subconsulta se ejecuta una vez por cada fila de la tabla `Cliente`.

---

# Caso 5. Importe total comprado por cliente

```sql
SELECT
    c.Nombre,
    (
        SELECT SUM(p.Total)
        FROM Pedido p
        WHERE p.IdCliente = c.IdCliente
    ) AS TotalComprado
FROM Cliente c
ORDER BY TotalComprado DESC;
```

Este tipo de informe aparece constantemente en cuadros de mando comerciales.

---

# Caso 6. Clientes que gastan por encima de la media

Este ejercicio combina varias ideas.

```sql
SELECT
    c.Nombre,
    (
        SELECT SUM(p.Total)
        FROM Pedido p
        WHERE p.IdCliente = c.IdCliente
    ) AS TotalGastado
FROM Cliente c
WHERE
(
    SELECT SUM(p.Total)
    FROM Pedido p
    WHERE p.IdCliente = c.IdCliente
)
>
(
    SELECT AVG(TotalCliente)
    FROM
    (
        SELECT
            SUM(Total) AS TotalCliente
        FROM Pedido
        GROUP BY IdCliente
    ) AS VentasClientes
);
```

Aunque la consulta es considerablemente más larga, ilustra cómo es posible combinar:

* subconsultas correlacionadas;
* subconsultas en `FROM`;
* funciones de agregación.

Este tipo de consultas ya se aproxima al nivel que encontramos en aplicaciones empresariales reales.

---

# Caso 7. Productos nunca vendidos

```sql
SELECT
    Nombre
FROM Producto pr
WHERE NOT EXISTS
(
    SELECT 1
    FROM DetallePedido dp
    WHERE dp.IdProducto = pr.IdProducto
);
```

Muy útil para detectar productos obsoletos o sin rotación.

---

# Caso 8. Categorías con productos caros

Mostrar únicamente las categorías que contienen al menos un producto cuyo precio supera los 1000 €.

```sql
SELECT
    c.Nombre
FROM Categoria c
WHERE EXISTS
(
    SELECT 1
    FROM Producto p
    WHERE p.IdCategoria = c.IdCategoria
      AND p.Precio > 1000
);
```

Aquí `EXISTS` evita tener que realizar un `JOIN` completo cuando únicamente nos interesa comprobar la existencia de productos que cumplan la condición.

---

## Reflexión final

A medida que aumenta la complejidad del problema, las subconsultas permiten dividir una consulta muy grande en pequeños bloques con una responsabilidad bien definida.

Esto hace que el código sea más fácil de leer, mantener y ampliar.

No obstante, siempre debemos vigilar el rendimiento cuando trabajamos con grandes volúmenes de datos.

---

## Ideas clave

* Las subconsultas permiten resolver problemas que serían difíciles mediante una única consulta plana.
* Es habitual combinar varios tipos de subconsultas en una misma sentencia SQL.
* `EXISTS` y `NOT EXISTS` simplifican enormemente las comprobaciones de existencia.
* Las subconsultas correlacionadas permiten calcular información específica para cada fila.
* En aplicaciones reales es frecuente encontrar consultas que mezclan `JOIN`, `GROUP BY` y varios niveles de subconsultas.

