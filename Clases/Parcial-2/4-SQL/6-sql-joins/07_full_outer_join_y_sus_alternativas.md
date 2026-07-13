# FULL OUTER JOIN y sus alternativas

## Introducción

Después de conocer `INNER JOIN`, `LEFT JOIN` y `RIGHT JOIN`, parece natural pensar que debería existir una unión que conserve ​**todas las filas de ambas tablas**​.

Efectivamente, el estándar SQL define esa operación con el nombre de ​**`FULL OUTER JOIN`**​.

Sin embargo, aquí encontramos una particularidad importante:

> **MySQL no implementa `FULL OUTER JOIN`.**

Por ello es necesario conocer tanto su funcionamiento teórico como las alternativas para conseguir el mismo resultado.

---

## ¿Qué hace FULL OUTER JOIN?

`FULL OUTER JOIN` devuelve:

* todas las filas de la tabla izquierda;
* todas las filas de la tabla derecha;
* las filas coincidentes aparecen combinadas;
* las filas sin coincidencia muestran `NULL` en las columnas de la otra tabla.

Es decir, combina el comportamiento de `LEFT JOIN` y `RIGHT JOIN`.

---

## Representación mediante conjuntos

```text
Tabla A

     ███████████
   ███████████████
  █████████████████
  █████████████████
   ███████████████
     ███████████
        Tabla B
```

Toda la unión de ambos conjuntos forma parte del resultado.

---

## Sintaxis en otros SGBD

En sistemas como PostgreSQL o SQL Server la consulta sería:

```sql
SELECT
    *
FROM Cliente
FULL OUTER JOIN Pedido
ON Cliente.IdCliente = Pedido.IdCliente;
```

MySQL devolverá un error porque esta sintaxis no está soportada.

---

## Alternativa en MySQL

La forma más habitual consiste en combinar un `LEFT JOIN` y un `RIGHT JOIN` mediante `UNION`.

```sql
SELECT
    c.Nombre,
    p.IdPedido
FROM Cliente AS c
LEFT JOIN Pedido AS p
ON c.IdCliente = p.IdCliente

UNION

SELECT
    c.Nombre,
    p.IdPedido
FROM Cliente AS c
RIGHT JOIN Pedido AS p
ON c.IdCliente = p.IdCliente;
```

`UNION` elimina automáticamente las filas duplicadas, obteniendo un resultado equivalente al `FULL OUTER JOIN`.

---

## ¿Por qué MySQL no lo implementa?

Históricamente, los desarrolladores de MySQL consideraron que la combinación de `LEFT JOIN`, `RIGHT JOIN` y `UNION` permitía resolver los mismos problemas sin añadir una nueva construcción al lenguaje.

Aunque esta decisión ha sido objeto de debate durante años, sigue vigente en las versiones actuales de MySQL.

---

## ¿Cuándo sería útil?

Un `FULL OUTER JOIN` resulta útil para:

* comparar dos listas de clientes;
* detectar registros existentes en una tabla pero no en otra;
* sincronizar bases de datos;
* realizar auditorías de información;
* encontrar diferencias entre conjuntos de datos.

---

## Comparación de los cuatro JOIN principales

| Tipo de JOIN    |  Conserva izquierda  |   Conserva derecha   |
| ----------------- | :---------------------: | :---------------------: |
| INNER JOIN      | ❌ Solo coincidencias | ❌ Solo coincidencias |
| LEFT JOIN       |          ✅          |          ❌          |
| RIGHT JOIN      |          ❌          |          ✅          |
| FULL OUTER JOIN |          ✅          |          ✅          |

Esta tabla resume el comportamiento fundamental de cada uno.

---

## Ideas clave

* `FULL OUTER JOIN` conserva todas las filas de ambas tablas.
* Forma parte del estándar SQL, pero ​**no está disponible en MySQL**​.
* En MySQL puede simularse combinando `LEFT JOIN`, `RIGHT JOIN` y `UNION`.
* Es especialmente útil para tareas de comparación, sincronización y auditoría de datos.
* Comprender su funcionamiento facilita trabajar con otros sistemas gestores de bases de datos como PostgreSQL, SQL Server u Oracle.

