# Subconsultas en WHERE

## Introducción

La ubicación más frecuente para una subconsulta es la cláusula `WHERE`.

En este caso, el resultado de la subconsulta se utiliza para decidir qué filas deben aparecer en la consulta principal.

La estructura general es:

```sql
SELECT ...
FROM ...
WHERE condición
(
    subconsulta
);
```

Esta técnica resulta extremadamente potente y aparece continuamente en aplicaciones empresariales.

---

## Ejemplo 1. Productos por encima de la media

```sql
SELECT
    Nombre,
    Precio
FROM Producto
WHERE Precio >
(
    SELECT AVG(Precio)
    FROM Producto
);
```

Proceso:

1. calcular el precio medio;
2. comparar cada producto con dicho valor;
3. mostrar únicamente los que lo superan.

---

## Ejemplo 2. Pedido más reciente

```sql
SELECT *
FROM Pedido
WHERE Fecha =
(
    SELECT MAX(Fecha)
    FROM Pedido
);
```

La subconsulta devuelve una única fecha.

La consulta principal busca todos los pedidos realizados exactamente en esa fecha.

---

## Ejemplo 3. Cliente con mayor identificador

```sql
SELECT *
FROM Cliente
WHERE IdCliente =
(
    SELECT MAX(IdCliente)
    FROM Cliente
);
```

Aunque este ejemplo no tiene demasiado interés práctico, permite comprender el funcionamiento del mecanismo.

---

## Utilizando operadores distintos

No estamos limitados al operador `=`.

También podemos utilizar:

```sql
<
>
<=
>=
<>
```

Por ejemplo:

```sql
SELECT
    Nombre,
    Precio
FROM Producto
WHERE Precio <
(
    SELECT AVG(Precio)
    FROM Producto
);
```

Obtendremos los productos cuyo precio sea inferior a la media.

---

## Subconsultas dentro de expresiones

También pueden combinarse con operaciones aritméticas.

```sql
SELECT
    Nombre,
    Precio
FROM Producto
WHERE Precio >
(
    SELECT AVG(Precio)
    FROM Producto
) * 1.25;
```

Aquí buscamos productos cuyo precio sea superior en un 25 % a la media.

---

## Ventajas

Las subconsultas en `WHERE` permiten:

* filtrar dinámicamente;
* evitar valores escritos manualmente;
* adaptar automáticamente la consulta cuando cambian los datos;
* construir informes mucho más flexibles.

---

## Limitaciones

Las subconsultas simples utilizadas con operadores como `=` o `>` deben devolver ​**un único valor**​.

Si devuelven varias filas, MySQL mostrará un error similar a:

```text
Subquery returns more than 1 row
```

Más adelante veremos cómo resolver este problema mediante:

* `IN`;
* `EXISTS`;
* `ANY`;
* `ALL`.

---

## Casos reales

Este patrón aparece constantemente en consultas como:

* productos más caros que la media;
* empleados con salario superior al promedio;
* ventas superiores al total medio;
* pedidos posteriores al último pedido de un cliente concreto;
* alumnos con una nota superior a la media del curso.

---

## Ideas clave

* `WHERE` es el lugar más habitual para utilizar subconsultas.
* La subconsulta suele proporcionar un valor utilizado para realizar comparaciones.
* Pueden utilizarse operadores relacionales y expresiones aritméticas.
* Si la subconsulta devuelve varias filas, será necesario utilizar otros operadores específicos que estudiaremos a continuación.

