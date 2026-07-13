# La consulta SELECT

## Introducción

La sentencia `SELECT` constituye el núcleo del lenguaje SQL.

Mientras que `INSERT`, `UPDATE` y `DELETE` modifican la información almacenada, `SELECT` permite recuperarla para que pueda ser mostrada, analizada o utilizada por una aplicación.

Es, con diferencia, la instrucción más utilizada en cualquier sistema gestor de bases de datos.

En muchos servidores empresariales, más del 90 % de las operaciones ejecutadas diariamente son consultas `SELECT`.

Aprender a construir buenas consultas será, por tanto, una de las competencias más importantes de toda la asignatura.

---

## ¿Qué hace SELECT?

`SELECT` recupera información almacenada en una o varias tablas.

No modifica la base de datos.

Simplemente devuelve un conjunto de resultados.

Visualmente:

```text
Base de datos

        │

        ▼

     SELECT

        │

        ▼

Tabla de resultados
```

La información original permanece intacta.

---

## La consulta más sencilla

Podemos recuperar todos los datos de una tabla utilizando:

```sql
SELECT *
FROM Cliente;
```

El símbolo `*` significa:

> "Todas las columnas de la tabla."

Si ejecutamos esta consulta podríamos obtener un resultado similar al siguiente.

| IdCliente | Nombre        | Ciudad    | Activo |
| ----------: | --------------- | ----------- | -------- |
|         1 | Ana Ruiz      | Santander | 1      |
|         2 | Luis Gómez   | Bilbao    | 1      |
|         3 | Javier Torres | Burgos    | 1      |

Cada fila representa un registro almacenado en la tabla.

Cada columna representa un atributo.

---

## SELECT no modifica datos

Una característica muy importante es que `SELECT` nunca altera la información.

Podemos ejecutar una misma consulta cientos de veces.

Los datos seguirán siendo exactamente los mismos.

Esto diferencia claramente al DQL del DML.

---

## SELECT como herramienta de trabajo

A partir de esta clase utilizaremos `SELECT` continuamente para:

* consultar clientes;
* visualizar productos;
* comprobar inserciones;
* verificar actualizaciones;
* analizar resultados;
* construir informes.

Incluso cuando ejecutemos operaciones `INSERT`, `UPDATE` o `DELETE`, normalmente terminaremos realizando un `SELECT` para comprobar el resultado.

---

## Ejemplo práctico

Consultar todos los productos.

```sql
SELECT *
FROM Producto;
```

Consultar todos los empleados.

```sql
SELECT *
FROM Empleado;
```

Consultar todas las categorías.

```sql
SELECT *
FROM Categoria;
```

Todas estas consultas siguen exactamente la misma estructura.

---

## ¿Qué devuelve una consulta?

Una consulta devuelve una ​**tabla temporal de resultados**​.

Esta tabla:

* existe únicamente durante la ejecución;
* puede contener todas o parte de las columnas;
* puede contener todas o parte de las filas;
* puede ordenarse de distintas formas.

Más adelante aprenderemos incluso a combinar varias tablas para generar resultados completamente nuevos.

---

## Buenas prácticas

Durante las primeras prácticas utilizaremos frecuentemente `SELECT *` porque facilita la comprensión de la estructura de las tablas.

Sin embargo, en proyectos profesionales suele recomendarse seleccionar únicamente las columnas necesarias.

Analizaremos esta recomendación en el siguiente apartado.

---

## Ideas clave

* `SELECT` recupera información de la base de datos.
* No modifica los datos almacenados.
* El resultado de una consulta es una tabla temporal.
* `SELECT *` devuelve todas las columnas de una tabla.
* La sentencia `SELECT` será la herramienta principal durante el resto del curso.

