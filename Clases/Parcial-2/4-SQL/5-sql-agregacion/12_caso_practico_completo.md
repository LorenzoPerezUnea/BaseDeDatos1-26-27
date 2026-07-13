# Caso práctico completo

## Introducción

A lo largo de esta clase hemos estudiado tres grandes bloques de funcionalidades:

* funciones de agregación;
* agrupaciones mediante `GROUP BY`;
* filtrado de grupos con `HAVING`;
* funciones de cadena;
* funciones numéricas;
* funciones de fecha;
* funciones de conversión.

En este caso práctico reuniremos todos estos conocimientos utilizando la base de datos de la empresa desarrollada durante las clases anteriores.

El objetivo no es únicamente escribir consultas correctas, sino también ​**interpretar la información obtenida**​, ya que en un entorno profesional SQL es una herramienta de análisis y apoyo a la toma de decisiones.

---

## Ejercicio 1. Número total de clientes

Obtener el número total de clientes registrados.

```sql
SELECT
    COUNT(*) AS TotalClientes
FROM Cliente;
```

Este tipo de consulta suele utilizarse para generar indicadores generales de la empresa.

---

## Ejercicio 2. Precio medio de los productos

Calcular el precio medio del catálogo.

```sql
SELECT
    ROUND(
        AVG(Precio),
        2
    ) AS PrecioMedio
FROM Producto;
```

La función `ROUND()` mejora la presentación del resultado mostrando únicamente dos decimales.

---

## Ejercicio 3. Valor total del inventario

Calcular el valor económico de todos los productos almacenados.

```sql
SELECT
    SUM(Precio * Stock) AS ValorInventario
FROM Producto;
```

En este ejemplo la función de agregación opera sobre una expresión y no únicamente sobre una columna.

---

## Ejercicio 4. Productos por categoría

Mostrar cuántos productos existen en cada categoría.

```sql
SELECT
    IdCategoria,
    COUNT(*) AS TotalProductos
FROM Producto
GROUP BY IdCategoria
ORDER BY TotalProductos DESC;
```

La ordenación permite identificar rápidamente las categorías con mayor número de productos.

---

## Ejercicio 5. Categorías con más de cinco productos

```sql
SELECT
    IdCategoria,
    COUNT(*) AS TotalProductos
FROM Producto
GROUP BY IdCategoria
HAVING COUNT(*) > 5;
```

Aquí aparece por primera vez la combinación de `GROUP BY` y `HAVING`.

---

## Ejercicio 6. Precio medio por categoría

```sql
SELECT
    IdCategoria,
    ROUND(
        AVG(Precio),
        2
    ) AS PrecioMedio
FROM Producto
GROUP BY IdCategoria
ORDER BY PrecioMedio DESC;
```

Este informe puede utilizarse para detectar categorías de productos de mayor valor.

---

## Ejercicio 7. Clientes por ciudad

```sql
SELECT
    Ciudad,
    COUNT(*) AS TotalClientes
FROM Cliente
GROUP BY Ciudad
ORDER BY TotalClientes DESC;
```

Es un ejemplo típico de informe comercial.

---

## Ejercicio 8. Clientes registrados durante el año actual

```sql
SELECT
    COUNT(*) AS NuevosClientes
FROM Cliente
WHERE YEAR(FechaRegistro) = YEAR(CURDATE());
```

La consulta combina una función de fecha con una función de agregación.

---

## Ejercicio 9. Nombre completo de los clientes

```sql
SELECT
    CONCAT(
        Nombre,
        ' ',
        Apellido
    ) AS Cliente
FROM Cliente;
```

Las funciones de cadena permiten mejorar la presentación de la información.

---

## Ejercicio 10. Antigüedad de los clientes

```sql
SELECT
    Nombre,
    DATEDIFF(
        CURDATE(),
        FechaRegistro
    ) AS DiasComoCliente
FROM Cliente
ORDER BY DiasComoCliente DESC;
```

Este informe puede utilizarse para identificar a los clientes más antiguos.

---

## Ejercicio integrador

Elabora una consulta que muestre:

* la categoría;
* el número de productos;
* el precio medio;
* el precio máximo;
* el precio mínimo.

Además:

* solo deben aparecer categorías con más de tres productos;
* el resultado debe ordenarse por precio medio descendente.

> **Este ejercicio integra prácticamente todos los contenidos desarrollados en esta sesión y constituye una excelente preparación para el estudio de las consultas con `JOIN`.**

---

## Ideas clave

* Las funciones de agregación permiten obtener indicadores empresariales.
* `GROUP BY` organiza la información por categorías o grupos.
* `HAVING` filtra los resultados agregados.
* Las funciones de cadena, numéricas y de fecha enriquecen las consultas.
* En aplicaciones reales es habitual combinar varias funciones dentro de una misma sentencia SQL.

