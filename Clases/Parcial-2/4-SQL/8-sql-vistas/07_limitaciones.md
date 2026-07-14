# Limitaciones

## Introducción

Las vistas son una herramienta muy potente, pero no resuelven todos los problemas.

Muchos estudiantes, después de descubrirlas, intentan utilizarlas para cualquier situación. Sin embargo, como cualquier otra característica de un SGBD, tienen limitaciones que conviene conocer.

Comprender estas limitaciones permitirá decidir cuándo una vista es la solución adecuada y cuándo debemos recurrir a otras herramientas, como tablas, procedimientos almacenados o consultas normales.

---

## 1. No almacenan los datos

La primera limitación es también su característica principal.

Una vista ​**no contiene los datos**​.

Únicamente almacena la consulta que permite obtenerlos.

Por ejemplo:

```sql
CREATE VIEW VistaProductos AS
SELECT
    Nombre,
    Precio
FROM Producto;
```

Cada vez que ejecutamos:

```sql
SELECT *
FROM VistaProductos;
```

MySQL vuelve a consultar la tabla `Producto`.

Esto significa que:

* si cambia la tabla, cambia la vista;
* si se elimina un registro, desaparece de la vista;
* si se inserta un registro nuevo, aparecerá automáticamente.

---

## 2. El rendimiento depende de la consulta

Una idea equivocada muy frecuente es pensar que una vista hace que una consulta sea más rápida.

No es cierto.

Si la consulta almacenada es compleja:

* muchos `JOIN`;
* subconsultas;
* funciones;
* agregaciones;

la vista seguirá necesitando ejecutar todo ese trabajo cada vez que se consulte.

La vista mejora la organización del código, pero no garantiza una mejora del rendimiento.

---

## 3. No todas son actualizables

Como vimos en el apartado anterior, muchas vistas son únicamente de lectura.

Por ejemplo, si utilizan:

* `GROUP BY`;
* `HAVING`;
* `DISTINCT`;
* funciones de agregación;
* determinadas combinaciones de `JOIN`.

En estos casos MySQL no puede determinar qué fila de la tabla original debe modificarse.

---

## 4. Dependencia de las tablas originales

Las vistas dependen completamente de las tablas sobre las que fueron creadas.

Supongamos:

```sql
CREATE VIEW VistaClientes AS
SELECT
    Nombre,
    Email
FROM Cliente;
```

Si posteriormente eliminamos la columna:

```text
Email
```

La vista dejará de funcionar correctamente.

Lo mismo ocurre si:

* cambia el nombre de una columna;
* se elimina una tabla;
* se modifica la estructura utilizada por la vista.

Por ello es importante mantener sincronizados el diseño de la base de datos y las vistas.

---

## 5. Complejidad excesiva

Es posible crear vistas basadas en otras vistas.

Por ejemplo:

```text
Vista A

↓

Vista B

↓

Vista C

↓

Vista D
```

Aunque técnicamente funciona, encadenar demasiadas vistas dificulta el mantenimiento y puede afectar al rendimiento.

Como regla general, conviene mantener una jerarquía sencilla.

---

## 6. No sustituyen un buen diseño

Las vistas no corrigen un modelo de datos mal diseñado.

Si una base de datos presenta:

* tablas redundantes;
* relaciones incorrectas;
* falta de normalización;

crear vistas no solucionará esos problemas.

Primero debe existir un buen diseño relacional.

---

## Recomendaciones

Utiliza vistas cuando:

* quieras simplificar consultas;
* necesites reutilizar código SQL;
* quieras limitar la información visible;
* desees mejorar la organización del proyecto.

No las utilices esperando resolver problemas de rendimiento o de diseño del modelo de datos.

---

## Ideas clave

* Las vistas no almacenan datos propios.
* El rendimiento depende de la consulta que contienen.
* Muchas vistas son de solo lectura.
* Dependen de la estructura de las tablas originales.
* No sustituyen un buen diseño de base de datos.

