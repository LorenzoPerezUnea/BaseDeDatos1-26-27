# WHERE

## Introducción

Hasta ahora todas las consultas realizadas devolvían **todos los registros** de una tabla.

Sin embargo, en una base de datos real esto rara vez resulta útil.

Imaginemos una empresa con:

* 500 000 clientes;
* 120 000 productos;
* 50 millones de pedidos.

Mostrar toda la información sería lento y poco práctico.

Lo habitual consiste en recuperar únicamente aquellos registros que cumplen una determinada condición.

Para ello utilizaremos la cláusula ​**`WHERE`**​, probablemente la herramienta más importante después de `SELECT`.

Durante las próximas clases aparecerá constantemente en prácticamente todas las consultas SQL.

---

## ¿Qué hace WHERE?

`WHERE` actúa como un filtro.

Selecciona únicamente las filas que cumplen una condición determinada.

Visualmente:

```text
Todos los clientes

        │

        ▼

     WHERE

Ciudad = 'Santander'

        │

        ▼

Solo clientes
de Santander
```

La tabla original no cambia.

Únicamente cambia el conjunto de resultados devuelto por la consulta.

---

## Sintaxis básica

La estructura general es:

```sql
SELECT
    columnas
FROM Tabla
WHERE condición;
```

Todo aquello que no cumpla la condición será descartado.

---

## Primer ejemplo

Queremos obtener únicamente los clientes de Santander.

```sql
SELECT *
FROM Cliente
WHERE Ciudad = 'Santander';
```

Resultado:

| Id | Nombre       | Ciudad    |
| ---: | -------------- | ----------- |
|  1 | Ana Ruiz     | Santander |
|  8 | Pedro López | Santander |
| 15 | Laura Díaz  | Santander |

Todos los clientes de otras ciudades quedan excluidos.

---

## Otro ejemplo

Consultar únicamente los productos activos.

```sql
SELECT
    Nombre,
    Precio
FROM Producto
WHERE Activo = TRUE;
```

Esta consulta devolverá únicamente los productos disponibles para su venta.

---

## WHERE no modifica datos

Es importante recordar que `WHERE` dentro de un `SELECT`​**no elimina registros**​.

Simplemente decide qué filas aparecerán en el resultado de la consulta.

La información continúa almacenada exactamente igual en la base de datos.

Esta diferencia resulta fundamental y evita confundir `SELECT ... WHERE` con sentencias como `DELETE ... WHERE` o `UPDATE ... WHERE`.

---

## Preparando los siguientes apartados

En este momento solo conocemos el operador de igualdad (`=`).

En los siguientes capítulos ampliaremos enormemente las posibilidades de `WHERE` mediante:

* operadores relacionales;
* operadores lógicos;
* `BETWEEN`;
* `IN`;
* `LIKE`;
* `IS NULL`.

Estas herramientas permitirán construir consultas muy precisas y potentes.

---

## Ideas clave

* `WHERE` filtra los registros devueltos por una consulta.
* No modifica la información almacenada.
* Solo aparecen las filas que cumplen la condición indicada.
* Es una de las cláusulas más utilizadas de todo SQL.
* Su potencia aumentará al combinarse con nuevos operadores en los siguientes apartados.

