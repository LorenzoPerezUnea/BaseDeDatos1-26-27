# Ejercicios incrementales

## Ejercicio 1: Clientes y pedidos

Queremos obtener el nombre de cada cliente junto con los identificadores y fechas de sus pedidos.

```
SELECT
    c.Nombre AS Cliente,
    p.IdPedido,
    p.Fecha
FROM Cliente AS c

INNER JOIN Pedido AS p
    ON c.IdCliente = p.IdCliente;
```

### Analizando la consulta

Comenzamos con dos tablas:

* `Cliente` contiene los datos personales de cada cliente.
* `Pedido` contiene los pedidos realizados.

La condición:

```
ON c.IdCliente = p.IdCliente
```

permite relacionar cada pedido con el cliente que lo ha realizado.

Utilizamos `INNER JOIN`, por lo que solamente aparecerán los clientes que tengan al menos un pedido.

Un cliente sin pedidos no aparecerá en el resultado.

---

## Ejercicio 2: Pedidos y empleados responsables

Queremos obtener el identificador y la fecha de cada pedido, junto con el nombre del empleado responsable.

```
SELECT
    p.IdPedido,
    p.Fecha,
    e.Nombre AS Empleado
FROM Pedido AS p

INNER JOIN Empleado AS e
    ON p.IdEmpleado = e.IdEmpleado;
```

### Analizando la consulta

En este caso relacionamos:

* `Pedido`, que contiene el identificador del empleado responsable.
* `Empleado`, que contiene su nombre y otros datos personales.

La relación se establece mediante `IdEmpleado`.

Es importante observar que no necesitamos utilizar `Cliente` para realizar esta consulta. Solamente incorporamos las tablas que aportan la información solicitada.

---

## Ejercicio 3: Pedidos y productos comprados

Queremos obtener los productos incluidos en cada pedido, indicando su cantidad.

```
SELECT
    dp.IdPedido,
    pr.Nombre AS Producto,
    dp.Cantidad
FROM DetallePedido AS dp

INNER JOIN Producto AS pr
    ON dp.IdProducto = pr.IdProducto;
```

### Analizando la consulta

Aquí intervienen dos tablas con funciones diferentes:

* `DetallePedido` almacena las líneas de cada pedido y la cantidad comprada.
* `Producto` contiene la información descriptiva de cada producto.

La tabla `DetallePedido` actúa como elemento intermedio entre los pedidos y los productos.

Esto es necesario porque un pedido puede contener varios productos y un producto puede aparecer en muchos pedidos.

---

## Ejercicio 4: Combinando tres tablas

Queremos obtener el identificador del pedido, el nombre del cliente y los productos incluidos en cada pedido.

```
SELECT
    c.Nombre AS Cliente,
    p.IdPedido,
    pr.Nombre AS Producto,
    dp.Cantidad
FROM Cliente AS c

INNER JOIN Pedido AS p
    ON c.IdCliente = p.IdCliente

INNER JOIN DetallePedido AS dp
    ON p.IdPedido = dp.IdPedido

INNER JOIN Producto AS pr
    ON dp.IdProducto = pr.IdProducto;
```

### Analizando la consulta

Ahora necesitamos relacionar cuatro tablas.

La construcción se realiza progresivamente:

1. `Cliente` se relaciona con `Pedido` mediante `IdCliente`.
2. `Pedido` se relaciona con `DetallePedido` mediante `IdPedido`.
3. `DetallePedido` se relaciona con `Producto` mediante `IdProducto`.

Cada nuevo `JOIN` incorpora información al resultado anterior.

Es importante comprender que no estamos realizando consultas independientes: cada operación utiliza el resultado de las relaciones anteriores y añade una nueva tabla.

Cada fila del resultado representa una línea de un pedido, identificando al cliente que lo realizó y el producto que compró.

---

## Ejercicio 5: Combinando varias relaciones

Queremos construir un informe que muestre el cliente, el empleado responsable, el pedido, el producto y su categoría.

```
SELECT
    c.Nombre AS Cliente,
    e.Nombre AS Empleado,
    p.IdPedido,
    p.Fecha,
    pr.Nombre AS Producto,
    ca.Nombre AS Categoria,
    dp.Cantidad
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

### Analizando la consulta

Esta consulta combina seis tablas y permite reconstruir información que se encuentra distribuida por todo el modelo relacional.

La secuencia de relaciones es:

1. `Cliente` con `Pedido`.
2. `Pedido` con `Empleado`.
3. `Pedido` con `DetallePedido`.
4. `DetallePedido` con `Producto`.
5. `Producto` con `Categoria`.

La cláusula `ORDER BY` ordena el resultado primero por fecha del pedido y después por nombre del cliente.

Observa que podemos incorporar tantos `JOIN` como sean necesarios para obtener la información solicitada, siempre que exista una relación que permita conectar las tablas.

---

## Ejercicio 6: JOIN con GROUP BY y funciones de agregación

Queremos calcular el importe total vendido por cada categoría de productos.

Para ello multiplicaremos la cantidad de cada línea por el precio del producto y sumaremos los importes correspondientes.

```
SELECT
    ca.Nombre AS Categoria,
    SUM(dp.Cantidad * pr.Precio) AS TotalVentas
FROM Categoria AS ca

INNER JOIN Producto AS pr
    ON ca.IdCategoria = pr.IdCategoria

INNER JOIN DetallePedido AS dp
    ON pr.IdProducto = dp.IdProducto

GROUP BY
    ca.IdCategoria,
    ca.Nombre

ORDER BY
    TotalVentas DESC;
```

### Analizando la consulta

En esta ocasión combinamos tres elementos:

* `JOIN` para relacionar categorías, productos y líneas de pedido.
* `SUM()` para calcular el importe total de las ventas.
* `GROUP BY` para agrupar los resultados por categoría.

La expresión:

```
dp.Cantidad * pr.Precio
```

calcula el importe de cada línea.

Posteriormente, `SUM()` acumula esos importes para cada categoría.

La cláusula:

```
GROUP BY ca.IdCategoria, ca.Nombre
```

hace que se obtenga una fila por categoría.

Finalmente, `ORDER BY TotalVentas DESC` muestra primero las categorías con mayor volumen de ventas.

---

## Ejercicio 7: LEFT JOIN con varias tablas y GROUP BY

El departamento comercial quiere conocer todos los empleados, incluyendo aquellos que todavía no han gestionado ningún pedido.

Para cada empleado queremos mostrar el número de pedidos gestionados y el importe total de las ventas correspondientes.

```
SELECT
    e.IdEmpleado,
    e.Nombre AS Empleado,
    COUNT(DISTINCT p.IdPedido) AS NumeroPedidos,
    COALESCE(
        SUM(dp.Cantidad * pr.Precio),
        0
    ) AS TotalVentas
FROM Empleado AS e

LEFT JOIN Pedido AS p
    ON e.IdEmpleado = p.IdEmpleado

LEFT JOIN DetallePedido AS dp
    ON p.IdPedido = dp.IdPedido

LEFT JOIN Producto AS pr
    ON dp.IdProducto = pr.IdProducto

GROUP BY
    e.IdEmpleado,
    e.Nombre

ORDER BY
    TotalVentas DESC;
```

### Analizando la consulta

En este ejercicio utilizamos varios `LEFT JOIN` consecutivos.

La primera relación conecta `Empleado` con `Pedido`.

Al utilizar `LEFT JOIN`, todos los empleados aparecerán en el resultado, incluso si no tienen pedidos asociados.

Después incorporamos:

* `DetallePedido`, para obtener las cantidades de los productos vendidos.
* `Producto`, para consultar los precios necesarios para calcular los importes.

Es importante utilizar `LEFT JOIN` también en las relaciones siguientes. De esta forma conservamos los empleados que no tienen pedidos y las filas sin detalles asociados.

### ¿Por qué utilizamos COUNT(DISTINCT)?

Un pedido puede contener varias líneas en `DetallePedido`.

Por tanto, si utilizáramos:

```
COUNT(p.IdPedido)
```

un mismo pedido podría contabilizarse varias veces.

Con:

```
COUNT(DISTINCT p.IdPedido)
```

cada pedido se cuenta una sola vez.

### ¿Para qué sirve COALESCE?

Un empleado sin ventas tendrá un resultado `NULL` en la suma.

Utilizamos:

```
COALESCE(SUM(dp.Cantidad * pr.Precio), 0)
```

para sustituir ese resultado nulo por cero.

Así podemos mostrar correctamente a los empleados que todavía no han generado ventas.

---

## Ejercicio 8: LEFT JOIN para localizar clientes sin pedidos

Queremos obtener todos los clientes que todavía no han realizado ningún pedido.

```
SELECT
    c.IdCliente,
    c.Nombre
FROM Cliente AS c

LEFT JOIN Pedido AS p
    ON c.IdCliente = p.IdCliente

WHERE p.IdPedido IS NULL;
```

### Analizando la consulta

Este es uno de los usos más habituales de `LEFT JOIN`.

Primero se relacionan todos los clientes con sus pedidos.

Como utilizamos `LEFT JOIN`, los clientes sin pedidos también permanecen en el resultado. En sus columnas correspondientes a `Pedido` aparecerán valores `NULL`.

Después aplicamos:

```
WHERE p.IdPedido IS NULL
```

para conservar únicamente aquellos registros que no tienen ningún pedido asociado.

Esta combinación permite localizar elementos de una tabla que no tienen correspondencia en otra.

---

## Ejercicio 9: Categorías sin ventas, incluyendo las que tienen productos sin vender

Queremos obtener todas las categorías, indicando el número de productos vendidos y el importe total de las ventas de cada categoría.

También deben aparecer las categorías que no tengan ningún producto vendido.

```
SELECT
    ca.IdCategoria,
    ca.Nombre AS Categoria,
    COUNT(DISTINCT dp.IdProducto) AS ProductosVendidos,
    COALESCE(
        SUM(dp.Cantidad * pr.Precio),
        0
    ) AS TotalVentas
FROM Categoria AS ca

LEFT JOIN Producto AS pr
    ON ca.IdCategoria = pr.IdCategoria

LEFT JOIN DetallePedido AS dp
    ON pr.IdProducto = dp.IdProducto

GROUP BY
    ca.IdCategoria,
    ca.Nombre

ORDER BY
    TotalVentas DESC;
```

### Analizando la consulta

La consulta comienza en `Categoria` y utiliza dos `LEFT JOIN`:

1. Se incorporan los productos de cada categoría.
2. Se incorporan las líneas de pedido correspondientes a cada producto.

Al utilizar `LEFT JOIN`, las categorías se mantienen aunque no tengan productos o aunque sus productos no aparezcan en ningún pedido.

La función `COUNT(DISTINCT dp.IdProducto)` cuenta los productos que aparecen en líneas de pedido, sin contar varias veces un mismo producto.

La función `COALESCE()` permite mostrar cero cuando no existen ventas.

Este ejercicio combina varias técnicas:

* relaciones entre tres tablas;
* `LEFT JOIN` consecutivos;
* funciones de agregación;
* `GROUP BY`;
* `ORDER BY`;
* tratamiento de valores `NULL`.
  

