# Integridad al insertar

## Introducción

En las clases anteriores aprendimos a definir restricciones como `PRIMARY KEY`, `FOREIGN KEY`, `NOT NULL`, `UNIQUE`, `CHECK` y `DEFAULT`.

Ahora que comenzamos a insertar información en nuestras tablas, veremos que todas esas restricciones empiezan a desempeñar su verdadera función.

Hasta este momento solo existían como parte de la estructura de la base de datos.

A partir de ahora serán las encargadas de impedir automáticamente que se almacenen datos incorrectos.

Una de las grandes ventajas de los sistemas gestores de bases de datos es que ​**la propia base de datos protege la información**​, incluso aunque una aplicación cometa errores.

---

## ¿Qué significa mantener la integridad?

Mantener la integridad significa garantizar que todos los registros almacenados cumplen las reglas del modelo de datos.

Por ejemplo:

* cada cliente posee un identificador único;
* ningún correo electrónico aparece duplicado;
* ningún producto tiene un precio negativo;
* un producto nunca referencia una categoría inexistente.

Todas estas comprobaciones son realizadas automáticamente por MySQL.

---

## PRIMARY KEY

Supongamos la siguiente tabla.

```text
Cliente

IdCliente (PK)

Nombre
```

Intentamos insertar:

```sql
INSERT INTO Cliente
(
    IdCliente,
    Nombre
)
VALUES
(
    1,
    'Carlos'
);
```

Si el identificador 1 ya existe, MySQL rechazará inmediatamente la operación.

La clave primaria garantiza la unicidad de cada registro.

---

## UNIQUE

Consideremos ahora la columna `CorreoElectronico`.

```sql
INSERT INTO Cliente
(
    Nombre,
    CorreoElectronico
)
VALUES
(
    'Ana',
    'ana@empresa.com'
);
```

Si ya existe otro cliente con ese mismo correo y la columna posee una restricción `UNIQUE`, la inserción será rechazada.

Esto evita duplicidades que podrían provocar numerosos problemas en la aplicación.

---

## NOT NULL

Las columnas definidas como `NOT NULL` siempre deben recibir un valor.

Por ejemplo:

```sql
INSERT INTO Categoria
(
    Nombre
)
VALUES
(
    NULL
);
```

MySQL mostrará un error indicando que la columna no admite valores nulos.

---

## CHECK

Supongamos que definimos la siguiente restricción.

```text
CHECK (Precio >= 0)
```

Ahora intentamos insertar:

```sql
INSERT INTO Producto
(
    Nombre,
    Precio,
    Stock,
    Activo
)
VALUES
(
    'Monitor',
    -150,
    5,
    TRUE
);
```

La operación será cancelada automáticamente porque el precio incumple la condición establecida.

---

## FOREIGN KEY

Las claves foráneas también participan durante las inserciones.

Supongamos que la tabla `Categoria` únicamente contiene los identificadores 1, 2 y 3.

Intentamos insertar:

```sql
INSERT INTO Producto
(
    Nombre,
    Precio,
    Stock,
    Activo,
    IdCategoria
)
VALUES
(
    'SSD 2 TB',
    199,
    20,
    TRUE,
    99
);
```

Como la categoría 99 no existe, MySQL rechazará la operación.

La integridad referencial impide crear relaciones inválidas.

---

## DEFAULT

Las restricciones no solo sirven para impedir errores.

También pueden facilitar las inserciones.

Si una columna posee un valor por defecto:

```text
Activo BOOLEAN DEFAULT TRUE
```

Podemos omitirla durante el `INSERT`.

MySQL asignará automáticamente el valor correspondiente.

---

## ¿Quién realiza todas estas comprobaciones?

Un aspecto muy importante es que ​**no es el programa quien valida los datos**​, sino el propio servidor MySQL.

Esto significa que:

* una aplicación web;
* un programa de escritorio;
* una aplicación móvil;
* un script SQL;
* phpMyAdmin;
* MySQL Workbench;

obtendrán exactamente el mismo comportamiento.

La integridad queda garantizada independientemente del programa utilizado para acceder a la base de datos.

---

## Errores frecuentes

Muchos principiantes intentan solucionar estos errores modificando las restricciones de la base de datos.

En realidad, normalmente el problema reside en los datos que intentan insertar.

La solución correcta consiste en revisar cuidadosamente la información antes de realizar la inserción y comprender qué restricción está siendo incumplida.

### Ideas clave

* Todas las restricciones se verifican automáticamente durante un `INSERT`.
* La base de datos protege la información frente a datos incorrectos.
* `PRIMARY KEY`, `UNIQUE`, `CHECK`, `NOT NULL` y `FOREIGN KEY` trabajan conjuntamente.
* Los valores `DEFAULT` simplifican las inserciones.
* La integridad es responsabilidad del servidor MySQL, no de la aplicación.

