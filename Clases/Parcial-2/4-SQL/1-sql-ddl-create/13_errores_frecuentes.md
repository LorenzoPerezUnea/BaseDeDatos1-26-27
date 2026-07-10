# Errores frecuentes

## Introducción

A lo largo de esta clase hemos aprendido a crear una base de datos, definir tablas, seleccionar tipos de datos y aplicar las primeras restricciones de integridad.

Aunque las sentencias estudiadas son relativamente sencillas, los errores que suelen cometer los estudiantes al comenzar a trabajar con SQL son muy similares año tras año.

Conocerlos de antemano permitirá evitarlos y comprender mejor los mensajes de error que devuelve MySQL.

Es importante recordar que un error no debe interpretarse como un fracaso, sino como una oportunidad para comprender mejor el funcionamiento del sistema gestor.

En programación y administración de bases de datos, aprender a interpretar los errores es una habilidad tan importante como escribir correctamente el código.

---

### Error 1. No seleccionar la base de datos

Uno de los errores más habituales consiste en crear una base de datos y comenzar inmediatamente a crear tablas.

Por ejemplo:

```sql
CREATE DATABASE empresa_tecnologica;

CREATE TABLE Cliente (

    IdCliente INT

);
```

Si no se ha seleccionado previamente la base de datos, MySQL mostrará un mensaje similar a:

```text
ERROR 1046 (3D000):
No database selected
```

La solución consiste en ejecutar previamente:

```sql
USE empresa_tecnologica;
```

---

### Error 2. Elegir tipos de datos incorrectos

Otro error muy frecuente consiste en utilizar el mismo tipo de dato para todas las columnas.

Por ejemplo:

```sql
Precio VARCHAR(50)
```

Aunque técnicamente es posible, impediría realizar correctamente operaciones matemáticas sobre los precios.

Del mismo modo, almacenar fechas como texto dificulta enormemente las consultas y los cálculos temporales.

Cada atributo debe utilizar el tipo de dato más adecuado para la información que representa.

---

### Error 3. Olvidar la clave primaria

Una tabla sin clave primaria puede almacenar información, pero resulta muy difícil identificar un registro concreto.

Por ejemplo:

```sql
CREATE TABLE Cliente (

    Nombre VARCHAR(100),

    Ciudad VARCHAR(80)

);
```

En esta situación nada impide insertar varios clientes exactamente iguales.

Durante este curso todas las entidades principales tendrán una clave primaria.

---

### Error 4. Insertar manualmente identificadores AUTO\_INCREMENT

Una vez definida una columna con `AUTO_INCREMENT`, no resulta necesario calcular manualmente el siguiente identificador.

Muchos estudiantes continúan escribiendo:

```sql
INSERT INTO Cliente
VALUES
(
    15,
    'Ana Ruiz',
    'ana@empresa.com',
    'Santander',
    '2026-09-15',
    TRUE
);
```

La práctica recomendada consiste en permitir que MySQL genere automáticamente dicho valor.

---

### Error 5. No comprobar los resultados

Una costumbre muy recomendable consiste en verificar inmediatamente cada modificación realizada.

Por ejemplo:

Después de crear una tabla:

```sql
SHOW TABLES;
```

Después de modificar su estructura:

```sql
DESC Cliente;
```

Después de insertar registros:

```sql
SELECT *
FROM Cliente;
```

Estas pequeñas comprobaciones permiten detectar errores en el mismo momento en que aparecen.

---

### Error 6. No leer los mensajes de error

Cuando MySQL devuelve un mensaje de error, muchos principiantes intentan modificar el código sin llegar a leer la explicación proporcionada por el servidor.

Sin embargo, la mayoría de los mensajes indican con bastante precisión cuál es el problema.

Por ejemplo:

* una tabla inexistente;
* una columna mal escrita;
* una restricción violada;
* un tipo de dato incompatible.

Acostumbrarse a interpretar estos mensajes reducirá considerablemente el tiempo necesario para depurar código.

---

### Error 7. No utilizar scripts

Otro error habitual consiste en ejecutar instrucciones aisladas y no conservarlas.

En un proyecto profesional, todas las sentencias SQL deben almacenarse en archivos para poder reconstruir la base de datos en cualquier momento.

A partir de esta clase comenzaremos a construir una colección de scripts que evolucionará durante todo el semestre.

---

### Ideas clave

* La mayoría de los errores iniciales pueden evitarse siguiendo una metodología ordenada.
* Siempre debe seleccionarse previamente la base de datos mediante `USE`.
* Elegir correctamente los tipos de datos mejora la calidad del diseño.
* Todas las entidades principales deben disponer de una clave primaria.
* `AUTO_INCREMENT` evita gestionar manualmente los identificadores.
* Verificar continuamente el resultado de cada operación facilita enormemente la detección de errores.
* Los scripts SQL constituyen una parte esencial de cualquier proyecto profesional.

