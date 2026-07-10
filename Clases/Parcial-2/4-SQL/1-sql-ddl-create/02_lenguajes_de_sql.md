# Los lenguajes de SQL

## Introducción

En el capítulo anterior vimos que SQL no es únicamente un lenguaje para realizar consultas. También permite crear bases de datos, modificar estructuras, administrar usuarios, controlar transacciones y gestionar la seguridad del sistema.

Esta amplitud de funciones hace que, en realidad, SQL no sea un único lenguaje, sino un conjunto de sublenguajes especializados. Cada uno de ellos está orientado a un tipo concreto de tareas y responde a una necesidad diferente dentro de la administración de una base de datos.

Conocer esta clasificación resulta muy útil porque permite comprender rápidamente el propósito de una instrucción SQL. Cuando un desarrollador observa una sentencia, normalmente puede identificar de inmediato a qué sublenguaje pertenece y qué efecto tendrá sobre la base de datos.

Durante este curso iremos estudiando estos sublenguajes de forma progresiva. En esta primera aproximación veremos su finalidad general y algunos ejemplos representativos.

### ¿Por qué dividir SQL en varios sublenguajes?

Imaginemos el trabajo cotidiano de una empresa.

Un administrador necesita crear nuevas tablas.

Un desarrollador necesita insertar pedidos.

Un analista debe consultar las ventas del último trimestre.

El responsable de sistemas necesita crear nuevos usuarios y asignar permisos.

Aunque todos utilizan SQL, las operaciones que realizan son completamente distintas.

Para facilitar su estudio, la comunidad ha agrupado las instrucciones SQL en varios bloques funcionales.

Esta clasificación no forma parte estrictamente de la sintaxis del lenguaje, pero se utiliza universalmente en libros, documentación técnica y cursos de formación.

### DDL: Data Definition Language

El **Lenguaje de Definición de Datos (DDL)** agrupa las instrucciones utilizadas para definir la estructura de la base de datos.

Permite crear, modificar y eliminar los objetos que forman parte del esquema.

Entre sus instrucciones más importantes se encuentran:

* `CREATE DATABASE`
* `CREATE TABLE`
* `ALTER TABLE`
* `DROP TABLE`
* `DROP DATABASE`
* `CREATE INDEX`
* `DROP INDEX`

Por ejemplo:

```sql
CREATE DATABASE EmpresaTecnologica;
```

o

```sql
CREATE TABLE Cliente (
    IdCliente INT PRIMARY KEY,
    Nombre VARCHAR(100)
);
```

Obsérvese que estas instrucciones no manipulan registros. Su objetivo consiste en definir la estructura sobre la que posteriormente se almacenará la información.

Durante las próximas clases trabajaremos casi exclusivamente con este sublenguaje.

### DML: Data Manipulation Language

Una vez creada la estructura, resulta necesario almacenar información.

Para ello se utiliza el ​**Lenguaje de Manipulación de Datos (DML)**​.

Las instrucciones más habituales son:

* `INSERT`
* `UPDATE`
* `DELETE`

Por ejemplo:

```sql
INSERT INTO Cliente
VALUES (1, 'Ana Ruiz');
```

o

```sql
UPDATE Cliente
SET Ciudad = 'Santander'
WHERE IdCliente = 1;
```

Estas instrucciones modifican el contenido de las tablas, pero no alteran su estructura.

Más adelante dedicaremos varias sesiones completas al estudio del DML.

### DQL: Data Query Language

Cuando la información ya se encuentra almacenada, el siguiente paso consiste en recuperarla.

Para ello se utiliza el ​**Lenguaje de Consulta de Datos (DQL)**​.

En la práctica, este sublenguaje está representado principalmente por una única instrucción:

```sql
SELECT
```

Aunque solo exista una palabra reservada principal, la enorme cantidad de cláusulas y posibilidades convierte a `SELECT` en una de las instrucciones más potentes de todo SQL.

Durante buena parte del semestre nos centraremos en aprender a construir consultas cada vez más complejas mediante esta instrucción.

### TCL: Transaction Control Language

Las bases de datos empresariales suelen ser utilizadas simultáneamente por cientos o miles de usuarios.

En estas situaciones resulta imprescindible controlar cuándo una operación debe hacerse permanente y cuándo debe deshacerse.

El **Lenguaje de Control de Transacciones (TCL)** proporciona precisamente estos mecanismos.

Las instrucciones más importantes son:

* `COMMIT`
* `ROLLBACK`
* `SAVEPOINT`

Por ejemplo, una aplicación bancaria puede realizar varias operaciones consecutivas y confirmar únicamente aquellas que se hayan completado correctamente.

El estudio detallado de las transacciones aparecerá en la parte final del curso.

### DCL: Data Control Language

Finalmente encontramos el ​**Lenguaje de Control de Datos (DCL)**​.

Su finalidad consiste en administrar los permisos de acceso a la base de datos.

Entre sus instrucciones destacan:

* `GRANT`
* `REVOKE`

Gracias a ellas es posible decidir qué usuarios pueden consultar información, modificar registros o crear nuevas tablas.

Aunque este tema suele corresponder a perfiles de administración de bases de datos, constituye un elemento esencial para garantizar la seguridad de los sistemas.

### Una visión global

Podemos resumir los distintos sublenguajes mediante la siguiente tabla.

| Sublenguaje | Finalidad               | Instrucciones habituales |
| ------------- | ------------------------- | -------------------------- |
| DDL         | Definir estructuras     | CREATE, ALTER, DROP      |
| DML         | Manipular registros     | INSERT, UPDATE, DELETE   |
| DQL         | Consultar información  | SELECT                   |
| TCL         | Controlar transacciones | COMMIT, ROLLBACK         |
| DCL         | Gestionar permisos      | GRANT, REVOKE            |

Esta clasificación servirá como referencia durante todo el resto del curso.

### Casos reales

En una misma jornada de trabajo un administrador de bases de datos puede utilizar todos estos sublenguajes.

Por ejemplo, puede crear una nueva tabla mediante DDL, insertar datos de prueba utilizando DML, comprobar el resultado mediante DQL, confirmar los cambios con TCL y finalmente asignar permisos utilizando DCL.

Aunque conceptualmente se estudien por separado, en la práctica forman parte del trabajo cotidiano con un sistema gestor de bases de datos.

### Errores frecuentes

Uno de los errores más habituales consiste en pensar que `SELECT` pertenece al mismo grupo que `INSERT` o `UPDATE`. Aunque todos manipulan información desde el punto de vista del usuario, tradicionalmente `SELECT` se clasifica dentro de DQL.

También es frecuente confundir DDL con DML. Una forma sencilla de diferenciarlos consiste en recordar que el DDL modifica la ​**estructura**​, mientras que el DML modifica los ​**datos**​.

### Ideas clave

* SQL puede dividirse en varios sublenguajes especializados.
* DDL define la estructura de la base de datos.
* DML manipula los registros almacenados.
* DQL permite consultar la información.
* TCL controla las transacciones.
* DCL administra la seguridad y los permisos de acceso.
* Esta clasificación facilita la comprensión y organización del lenguaje SQL.

