# Vistas actualizables

## Introducción

Hasta ahora hemos utilizado las vistas únicamente para realizar consultas.

Sin embargo, surge una pregunta muy interesante:

> **¿Es posible insertar, modificar o eliminar datos utilizando una vista?**

La respuesta es:

**Sí, pero no siempre.**

Algunas vistas permiten ejecutar instrucciones como:

```sql
INSERT
UPDATE
DELETE
```

mientras que otras son exclusivamente de lectura.

Comprender esta diferencia resulta fundamental para utilizar correctamente las vistas.

---

## Una vista sencilla

Supongamos la siguiente vista:

```sql
CREATE VIEW VistaProductos AS
SELECT
    IdProducto,
    Nombre,
    Precio
FROM Producto;
```

La vista hace referencia a una única tabla y no realiza cálculos ni agrupaciones.

Podemos consultar:

```sql
SELECT *
FROM VistaProductos;
```

Pero también podremos modificar datos.

---

## Actualizar datos

```sql
UPDATE VistaProductos
SET Precio = 499.90
WHERE IdProducto = 10;
```

Aunque estamos actualizando la vista, en realidad MySQL modifica la tabla `Producto`.

---

## Insertar registros

También es posible insertar nuevos registros.

```sql
INSERT INTO VistaProductos
(Nombre, Precio)
VALUES
('Teclado Mecánico', 89.95);
```

El nuevo producto aparecerá en la tabla original.

---

## Eliminar registros

```sql
DELETE
FROM VistaProductos
WHERE IdProducto = 10;
```

Nuevamente, el registro se elimina realmente de la tabla `Producto`.

---

## ¿Cuándo una vista deja de ser actualizable?

No todas las vistas permiten estas operaciones.

Por ejemplo:

```sql
CREATE VIEW VistaVentas AS
SELECT
    c.Nombre,
    SUM(p.Total) AS TotalVentas
FROM Cliente c
JOIN Pedido p
ON c.IdCliente = p.IdCliente
GROUP BY c.Nombre;
```

Esta vista contiene:

* `JOIN`;
* `SUM()`;
* `GROUP BY`.

No representa directamente una fila de una tabla.

Por ello MySQL no sabe exactamente qué registro debería modificar.

En consecuencia, la vista pasa a ser ​**solo de lectura**​.

---

## Regla general

Como criterio inicial, una vista suele ser actualizable cuando:

* se basa en una única tabla;
* no utiliza funciones de agregación;
* no contiene `GROUP BY`;
* no utiliza `DISTINCT`;
* no genera columnas calculadas complejas.

Más adelante estudiaremos con mayor detalle todas estas restricciones.

---

## ¿Es recomendable actualizar mediante vistas?

Aunque es posible, en la mayoría de los proyectos las vistas se utilizan principalmente para consultas.

Las operaciones `INSERT`, `UPDATE` y `DELETE` suelen realizarse directamente sobre las tablas o mediante procedimientos almacenados.

No obstante, conocer esta posibilidad ayuda a comprender mejor el funcionamiento interno de las vistas.

---

## Ideas clave

* Algunas vistas permiten insertar, actualizar y eliminar datos.
* Las modificaciones realizadas sobre la vista afectan a la tabla original.
* Las vistas con agregaciones, agrupaciones o consultas complejas suelen ser de solo lectura.
* No todas las vistas son actualizables.
* Antes de modificar datos mediante una vista conviene comprobar si cumple las condiciones necesarias.

