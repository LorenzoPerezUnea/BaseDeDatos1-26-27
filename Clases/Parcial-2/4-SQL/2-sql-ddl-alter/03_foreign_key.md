# FOREIGN KEY

## Introducción

Hasta este momento todas las tablas de nuestro proyecto eran independientes.

Podíamos crear clientes, productos o categorías, pero la base de datos no conocía ninguna relación entre ellas.

Sin embargo, el modelo relacional se caracteriza precisamente por permitir que las distintas entidades estén conectadas entre sí.

Por ejemplo:

* un producto pertenece a una categoría;
* un pedido pertenece a un cliente;
* una línea de pedido pertenece simultáneamente a un pedido y a un producto.

Estas relaciones se implementan mediante una de las restricciones más importantes de cualquier base de datos relacional: la **clave foránea** o ​**FOREIGN KEY**​.

A partir de este capítulo nuestro modelo comenzará a comportarse como una auténtica base de datos relacional.

---

### ¿Qué es una clave foránea?

Una clave foránea es una columna cuyo valor debe existir previamente como clave primaria en otra tabla.

Dicho de otra forma, una clave foránea establece una referencia entre dos tablas.

Por ejemplo:

```text
Categoria

IdCategoria
Nombre

        ▲

        │

Producto

IdProducto
Nombre
IdCategoria
```

Cada producto almacenará el identificador de una categoría existente.

Gracias a esta relación, la base de datos impedirá registrar productos asociados a categorías inexistentes.

---

### Tabla padre y tabla hija

En una relación intervienen siempre dos tablas.

| Concepto    | Tabla                   |
| ------------- | ------------------------- |
| Tabla padre | Contiene la PRIMARY KEY |
| Tabla hija  | Contiene la FOREIGN KEY |

En nuestro ejemplo:

* **Categoria** es la tabla padre.
* **Producto** es la tabla hija.

La tabla hija depende de la existencia de registros en la tabla padre.

Esta terminología será utilizada durante todo el curso.

---

### Creando las tablas

Comenzaremos creando la tabla `Categoria`.

```sql
CREATE TABLE Categoria (

    IdCategoria INT AUTO_INCREMENT PRIMARY KEY,

    Nombre VARCHAR(80) NOT NULL

);
```

Posteriormente crearemos `Producto`.

Por el momento únicamente añadiremos la nueva columna.

```sql
CREATE TABLE Producto (

    IdProducto INT AUTO_INCREMENT PRIMARY KEY,

    Nombre VARCHAR(120) NOT NULL,

    Precio DECIMAL(10,2) NOT NULL,

    IdCategoria INT

);
```

Todavía no existe ninguna relación.

Simplemente hemos añadido una columna cuyo nombre coincide con la clave primaria de la otra tabla.

En la siguiente sección aprenderemos a convertir esa columna en una auténtica clave foránea.

### Ideas clave

* Una clave foránea conecta dos tablas del modelo relacional.
* Siempre referencia una clave primaria existente.
* Permite representar relaciones entre entidades.
* Introduce el concepto de tabla padre y tabla hija.
* Constituye la base de la integridad referencial que estudiaremos en los siguientes capítulos.

