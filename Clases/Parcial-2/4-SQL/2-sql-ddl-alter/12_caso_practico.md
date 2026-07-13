# Caso práctico

## Introducción

A lo largo de esta clase hemos estudiado las principales restricciones del modelo relacional y aprendido a modificar la estructura de una base de datos mediante `ALTER TABLE`.

Ha llegado el momento de aplicar todos estos conocimientos sobre la base de datos que comenzamos a construir en la clase anterior.

En lugar de crear nuevas tablas desde cero, trabajaremos exactamente igual que lo haría un administrador de bases de datos en una empresa: ​**evolucionando un esquema ya existente**​.

Nuestro objetivo será enriquecer el modelo incorporando nuevas columnas, nuevas restricciones y la primera relación entre tablas.

---

## Situación inicial

Partimos del esquema construido en la clase 14.

```text
Cliente

IdCliente
Nombre
CorreoElectronico
Ciudad
FechaRegistro
Activo


Categoria

IdCategoria
Nombre
Descripcion


Producto

IdProducto
Nombre
Precio
Stock
Activo


Empleado

IdEmpleado
Nombre
Cargo
FechaContratacion
Activo
```

Las tablas existen, pero todavía presentan dos limitaciones importantes:

* algunas restricciones aún no se han definido;
* las tablas siguen siendo independientes.

Nuestro trabajo consistirá en mejorar progresivamente este diseño.

---

## Paso 1. Añadir una nueva columna

El departamento comercial solicita almacenar el teléfono de cada cliente.

Realizamos la modificación.

```sql
ALTER TABLE Cliente

ADD COLUMN Telefono VARCHAR(20);
```

Comprobamos el resultado.

```sql
DESC Cliente;
```

La nueva columna aparece al final de la tabla.

---

## Paso 2. Garantizar correos únicos

Hasta ahora era posible registrar varios clientes utilizando el mismo correo electrónico.

Añadimos la restricción correspondiente.

```sql
ALTER TABLE Cliente

ADD CONSTRAINT UQ_Cliente_Correo

UNIQUE (CorreoElectronico);
```

A partir de este momento cada dirección de correo podrá utilizarse una única vez.

---

## Paso 3. Añadir una validación al precio

Queremos impedir que existan productos con precios negativos.

```sql
ALTER TABLE Producto

ADD CONSTRAINT CHK_Producto_Precio

CHECK (Precio >= 0);
```

Ahora cualquier intento de registrar un precio inferior a cero será rechazado automáticamente.

---

## Paso 4. Preparar la relación con Categoría

Nuestra tabla `Producto` todavía no dispone de la columna necesaria para relacionarse con `Categoria`.

La añadimos.

```sql
ALTER TABLE Producto

ADD COLUMN IdCategoria INT;
```

Verificamos la estructura.

```sql
DESC Producto;
```

Ya podemos observar el nuevo atributo.

Sin embargo, todavía no existe ninguna relación real.

---

## Paso 5. Crear la clave foránea

Convertimos la nueva columna en una clave foránea.

```sql
ALTER TABLE Producto

ADD CONSTRAINT FK_Producto_Categoria

FOREIGN KEY (IdCategoria)

REFERENCES Categoria(IdCategoria)

ON DELETE RESTRICT

ON UPDATE RESTRICT;
```

A partir de este momento la integridad referencial comienza a proteger automáticamente nuestro modelo.

---

## Paso 6. Verificar el esquema

Podemos consultar la definición completa de la tabla.

```sql
SHOW CREATE TABLE Producto;
```

Observaremos:

* la clave primaria;
* la nueva columna `IdCategoria`;
* la restricción `CHECK`;
* la clave foránea;
* las acciones `ON DELETE` y `ON UPDATE`.

Por primera vez nuestro modelo empieza a parecerse a una base de datos profesional.

---

## Resultado final

El esquema queda representado de la siguiente manera.

```text
Categoria

IdCategoria (PK)

Nombre

Descripcion

        ▲
        │
        │ FK
        │

Producto

IdProducto (PK)

Nombre

Precio

Stock

Activo

IdCategoria (FK)
```

Ya no tenemos simplemente cuatro tablas independientes.

Disponemos de un modelo relacional donde una entidad depende de otra y donde la propia base de datos garantiza la consistencia de la información.

---

## Lo aprendido

En este caso práctico hemos utilizado prácticamente todas las operaciones estudiadas durante la clase:

* `ALTER TABLE`
* `ADD COLUMN`
* `ADD CONSTRAINT`
* `UNIQUE`
* `CHECK`
* `FOREIGN KEY`
* `SHOW CREATE TABLE`
* `DESC`

Este será el procedimiento habitual durante el resto del curso: ampliar progresivamente el mismo proyecto sin reconstruir continuamente la base de datos.

---

## Ideas clave

* Las bases de datos evolucionan mediante modificaciones incrementales.
* `ALTER TABLE` permite adaptar el esquema sin perder información.
* Las restricciones protegen automáticamente la calidad de los datos.
* La primera clave foránea del curso conecta `Producto` con `Categoria`.
* El caso práctico seguirá creciendo sobre este mismo esquema en las próximas clases.

