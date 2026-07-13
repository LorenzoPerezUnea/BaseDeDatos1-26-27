# ADD CONSTRAINT

## Introducción

En las secciones anteriores hemos aprendido a modificar la estructura de una tabla utilizando `ALTER TABLE`. Hemos añadido columnas, modificado su definición e incluso eliminado aquellas que ya no eran necesarias.

Sin embargo, las columnas no son el único elemento que puede evolucionar con el tiempo.

También es muy frecuente que una tabla inicialmente creada sin determinadas restricciones necesite incorporarlas posteriormente.

Por ejemplo:

* añadir una clave foránea cuando aparece una nueva relación;
* impedir valores duplicados mediante `UNIQUE`;
* establecer una condición mediante `CHECK`.

En todos estos casos utilizaremos la cláusula ​**ADD CONSTRAINT**​.

Esta operación resulta especialmente habitual cuando una base de datos ha ido creciendo de forma progresiva, exactamente igual que está ocurriendo con nuestro caso práctico.

---

### ¿Qué es una restricción con nombre?

Aunque MySQL permite crear algunas restricciones sin asignarles un nombre explícito, en proyectos profesionales es recomendable nombrarlas siempre.

Por ejemplo:

```text
PK_Cliente

FK_Producto_Categoria

UQ_Cliente_Correo

CHK_Producto_Precio
```

Asignar nombres facilita enormemente el mantenimiento.

Si en el futuro fuera necesario modificar o eliminar una restricción, podremos referirnos a ella directamente.

---

### Sintaxis general

La estructura básica es:

```sql
ALTER TABLE NombreTabla

ADD CONSTRAINT NombreRestriccion

TipoRestriccion (...);
```

La parte final dependerá del tipo de restricción que deseemos crear.

---

### Añadiendo una restricción UNIQUE

Supongamos que la tabla `Cliente` ya existe y queremos impedir que dos clientes compartan el mismo correo electrónico.

Podemos hacerlo mediante:

```sql
ALTER TABLE Cliente

ADD CONSTRAINT UQ_Cliente_Correo

UNIQUE (CorreoElectronico);
```

A partir de ese momento MySQL rechazará cualquier intento de insertar un correo ya existente.

---

### Añadiendo una restricción CHECK

También podemos incorporar nuevas reglas de validación.

Por ejemplo:

```sql
ALTER TABLE Producto

ADD CONSTRAINT CHK_Producto_Precio

CHECK (Precio >= 0);
```

Esta comprobación comenzará a aplicarse inmediatamente sobre las futuras inserciones y modificaciones.

---

### Añadiendo una clave foránea

Uno de los usos más habituales consiste en conectar tablas que inicialmente eran independientes.

Supongamos que la tabla `Producto` ya dispone de una columna `IdCategoria`.

Ahora queremos convertirla en una clave foránea.

```sql
ALTER TABLE Producto

ADD CONSTRAINT FK_Producto_Categoria

FOREIGN KEY (IdCategoria)

REFERENCES Categoria(IdCategoria);
```

En este momento queda establecida oficialmente la relación entre ambas tablas.

A partir de ahora ningún producto podrá referenciar una categoría inexistente.

---

### ¿Qué ocurre si existen datos incorrectos?

Antes de crear una restricción, MySQL verifica que todos los datos actuales la cumplen.

Por ejemplo, si intentamos crear la clave foránea anterior pero existen productos cuyo `IdCategoria` no aparece en la tabla `Categoria`, la operación será rechazada.

Esto constituye una importante medida de protección.

No basta con que las futuras inserciones sean correctas.

Toda la información existente debe respetar la nueva regla.

---

### Casos reales

En proyectos profesionales es muy habitual crear inicialmente un esquema sencillo e ir incorporando restricciones conforme madura la aplicación.

Por ello, `ADD CONSTRAINT` aparece constantemente en scripts de migración y herramientas como Flyway o Liquibase.

Comprender esta sentencia permitirá entender posteriormente cómo evolucionan las bases de datos reales.

---

### Errores frecuentes

Uno de los errores más comunes consiste en intentar crear una restricción sobre datos que ya contienen inconsistencias.

También es frecuente no asignar nombres a las restricciones, dificultando su mantenimiento posterior.

Finalmente, muchos estudiantes olvidan comprobar si la tabla referenciada existe antes de crear una clave foránea.

### Ideas clave

* `ADD CONSTRAINT` incorpora restricciones a tablas ya existentes.
* Es recomendable asignar siempre un nombre descriptivo a cada restricción.
* Puede utilizarse para crear restricciones `UNIQUE`, `CHECK` y `FOREIGN KEY`.
* MySQL verifica que los datos existentes cumplen la nueva restricción.
* Esta operación resulta habitual durante la evolución de aplicaciones profesionales.

