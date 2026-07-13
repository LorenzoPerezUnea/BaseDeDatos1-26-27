# Caso práctico

## Introducción

Después de estudiar todos los componentes básicos de la sentencia `SELECT`, es el momento de aplicarlos conjuntamente sobre la base de datos de la empresa tecnológica.

El objetivo de este caso práctico es demostrar que las consultas reales suelen combinar varias cláusulas al mismo tiempo.

Trabajaremos con las tablas:

* `Cliente`
* `Producto`
* `Categoria`
* `Empleado`

Todas ellas fueron creadas y pobladas en las clases anteriores.

---

## Ejercicio 1. Mostrar todos los clientes

Obtener toda la información de la tabla `Cliente`.

```sql
SELECT *
FROM Cliente;
```

Este tipo de consulta resulta útil para inspeccionar rápidamente una tabla durante el desarrollo.

---

## Ejercicio 2. Mostrar únicamente determinadas columnas

Consultar únicamente el nombre y la ciudad de los clientes.

```sql
SELECT
    Nombre,
    Ciudad
FROM Cliente;
```

Observamos cómo la proyección permite mostrar únicamente la información necesaria.

---

## Ejercicio 3. Utilizar alias

Mostrar el nombre del cliente y su ciudad utilizando encabezados más descriptivos.

```sql
SELECT
    Nombre AS Cliente,
    Ciudad AS CiudadResidencia
FROM Cliente;
```

Los alias mejoran considerablemente la presentación de informes.

---

## Ejercicio 4. Filtrar productos

Consultar únicamente los productos cuyo precio sea superior a 200 €.

```sql
SELECT
    Nombre,
    Precio
FROM Producto
WHERE Precio > 200;
```

Aquí utilizamos conjuntamente `SELECT` y `WHERE`.

---

## Ejercicio 5. Combinar varias condiciones

Mostrar únicamente los productos activos cuyo stock sea superior a 10 unidades.

```sql
SELECT
    Nombre,
    Precio,
    Stock
FROM Producto
WHERE
    Activo = TRUE
    AND Stock > 10;
```

Este tipo de consulta es muy habitual en sistemas de inventario.

---

## Ejercicio 6. Buscar mediante LIKE

Mostrar todos los clientes cuyo nombre comience por la letra ​**A**​.

```sql
SELECT
    Nombre
FROM Cliente
WHERE Nombre LIKE 'A%';
```

---

## Ejercicio 7. Ordenar resultados

Mostrar todos los productos ordenados de mayor a menor precio.

```sql
SELECT
    Nombre,
    Precio
FROM Producto
ORDER BY Precio DESC;
```

La ordenación facilita enormemente la interpretación de los resultados.

---

## Ejercicio 8. Obtener los tres productos más caros

```sql
SELECT
    Nombre,
    Precio
FROM Producto
ORDER BY Precio DESC
LIMIT 3;
```

En una única consulta hemos utilizado:

* `SELECT`;
* `ORDER BY`;
* `LIMIT`.

Este patrón aparece constantemente en aplicaciones reales.

---

## Ejercicio integrador

Construye una consulta que cumpla simultáneamente las siguientes condiciones:

* mostrar únicamente el nombre y el precio;
* incluir solo productos activos;
* precio entre 100 y 1000 euros;
* ordenar de mayor a menor precio;
* mostrar únicamente los cinco primeros resultados.

Este ejercicio combina la mayoría de los conceptos estudiados durante la clase y sirve como preparación para las próximas sesiones, donde comenzaremos a trabajar con funciones de agregación y consultas mucho más avanzadas.

---

## Ideas clave

* Las consultas reales suelen combinar varias cláusulas en una única sentencia.
* El orden lógico de ejecución sigue siendo el mismo independientemente de la complejidad de la consulta.
* Cuanto más dominemos `SELECT`, más sencillo resultará aprender `JOIN`, `GROUP BY` y el resto de SQL.

