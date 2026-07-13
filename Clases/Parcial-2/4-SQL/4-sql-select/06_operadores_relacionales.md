# Operadores relacionales

## Introducción

En el apartado anterior aprendimos que la cláusula `WHERE` permite filtrar los registros de una consulta.

Sin embargo, hasta el momento únicamente hemos utilizado el operador de igualdad (`=`).

En la práctica necesitaremos realizar comparaciones mucho más variadas.

Por ejemplo:

* productos cuyo precio sea superior a 500 €;
* clientes registrados después de una determinada fecha;
* empleados distintos de un cargo concreto;
* productos cuyo stock sea inferior a 10 unidades.

Para resolver estos problemas SQL incorpora los ​**operadores relacionales**​, que permiten comparar valores de distintos tipos de datos.

Estos operadores proceden directamente de la lógica matemática y del Álgebra Relacional estudiada al comienzo del curso.

---

## Operadores disponibles

Los operadores relacionales más utilizados son los siguientes.

| Operador | Significado       |
| ---------- | ------------------- |
| =        | Igual que         |
| <>       | Distinto de       |
| >        | Mayor que         |
| >=       | Mayor o igual que |
| <        | Menor que         |
| <=       | Menor o igual que |

Todos ellos producen un resultado lógico:

* Verdadero (`TRUE`)
* Falso (`FALSE`)

Solo las filas cuya condición sea verdadera aparecerán en el resultado de la consulta.

---

## Igualdad (=)

El operador más sencillo compara dos valores buscando coincidencias exactas.

```sql
SELECT *
FROM Categoria
WHERE Nombre = 'Portátiles';
```

Resultado:

| IdCategoria | Nombre      |
| ------------: | ------------- |
|           1 | Portátiles |

Es importante recordar que, en columnas de texto, la comparación depende de la intercalación (​*collation*​) configurada en la base de datos.

---

## Distinto (<>)

Permite recuperar todos los registros cuyo valor sea diferente.

```sql
SELECT
    Nombre,
    Ciudad
FROM Cliente
WHERE Ciudad <> 'Santander';
```

Resultado:

| Nombre         | Ciudad |
| ---------------- | -------- |
| Luis Gómez    | Bilbao |
| Javier Torres  | Burgos |
| Elena Sánchez | León  |

Todos los clientes de Santander quedan excluidos.

---

## Mayor y menor

Supongamos que queremos consultar los productos con un precio superior a 500 euros.

```sql
SELECT
    Nombre,
    Precio
FROM Producto
WHERE Precio > 500;
```

También podemos buscar productos económicos.

```sql
SELECT
    Nombre,
    Precio
FROM Producto
WHERE Precio < 100;
```

Los operadores funcionan igualmente con fechas y números enteros.

---

## Mayor o igual y menor o igual

Estos operadores incluyen el propio límite.

```sql
SELECT *
FROM Producto
WHERE Stock >= 20;
```

o bien:

```sql
SELECT *
FROM Producto
WHERE Precio <= 300;
```

La diferencia entre `>` y `>=` puede parecer pequeña, pero resulta muy importante cuando el valor límite también debe formar parte del resultado.

---

## Comparando fechas

Los operadores relacionales funcionan igualmente con fechas.

```sql
SELECT
    Nombre,
    FechaRegistro
FROM Cliente
WHERE FechaRegistro >= '2026-01-01';
```

La consulta recuperará todos los clientes registrados a partir del 1 de enero de 2026.

---

## Comparando valores booleanos

También pueden utilizarse con columnas lógicas.

```sql
SELECT *
FROM Producto
WHERE Activo = TRUE;
```

o bien:

```sql
SELECT *
FROM Producto
WHERE Activo = FALSE;
```

Este tipo de consultas aparece constantemente en aplicaciones empresariales.

---

## Errores frecuentes

Entre los errores más habituales encontramos:

* utilizar `=` cuando realmente se desea `>=`;
* olvidar que `<>` significa "distinto";
* comparar valores incompatibles, como texto con números;
* escribir fechas con un formato incorrecto.

La mejor forma de evitar estos errores consiste en leer la condición como si fuera una frase en lenguaje natural antes de ejecutarla.

---

## Ideas clave

* Los operadores relacionales comparan valores.
* Funcionan con números, texto, fechas y valores booleanos.
* Devuelven un resultado lógico (`TRUE` o `FALSE`).
* Constituyen la base de prácticamente todas las cláusulas `WHERE`.
* Su potencia aumentará todavía más al combinarlos con operadores lógicos.

