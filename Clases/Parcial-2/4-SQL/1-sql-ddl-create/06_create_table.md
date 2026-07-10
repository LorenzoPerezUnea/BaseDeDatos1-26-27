# CREATE TABLE

## Introducción

Ya disponemos de una base de datos y conocemos los tipos de datos que utilizaremos durante el resto del curso.

El siguiente paso consiste en crear nuestra primera tabla.

En MySQL las tablas se crean mediante la sentencia ​**CREATE TABLE**​, una de las instrucciones más importantes del lenguaje DDL.

Durante las próximas clases construiremos progresivamente todas las tablas del caso práctico. Comenzaremos con una versión sencilla de la tabla ​**Cliente**​, que posteriormente irá evolucionando conforme aparezcan nuevos conceptos como claves foráneas, índices y restricciones de integridad.

---

### Sintaxis general

La estructura básica de una sentencia `CREATE TABLE` es la siguiente.

```sql
CREATE TABLE NombreTabla (

    Columna1 TipoDato,

    Columna2 TipoDato,

    Columna3 TipoDato

);
```

Entre los paréntesis se define la estructura completa de la tabla.

Cada línea describe una columna indicando su nombre y el tipo de dato correspondiente.

---

### Nuestra primera tabla

Crearemos la tabla ​**Cliente**​.

Ejecute la siguiente sentencia.

```sql
CREATE TABLE Cliente (

    IdCliente INT,

    Nombre VARCHAR(100),

    CorreoElectronico VARCHAR(150),

    Ciudad VARCHAR(80),

    FechaRegistro DATE

);
```

Si la ejecución finaliza correctamente, MySQL mostrará un mensaje similar a:

```text
Query OK, 0 rows affected
```

Aunque todavía no exista ningún registro, la tabla ya forma parte del esquema de la base de datos.

---

### Comprobando la creación

Como en todas las operaciones DDL, es recomendable verificar inmediatamente el resultado.

Podemos listar todas las tablas del esquema mediante:

```sql
SHOW TABLES;
```

El resultado será similar a:

| Tables\_in\_empresa\_tecnologica |
| ---------------------------------- |
| Cliente                          |

También podemos consultar la estructura de la tabla.

```sql
DESCRIBE Cliente;
```

o de forma abreviada:

```sql
DESC Cliente;
```

Obtendremos una salida similar a:

| Field             | Type         | Null | Key | Default | Extra |
| ------------------- | -------------- | ------ | ----- | --------- | ------- |
| IdCliente         | int          | YES  |     | NULL    |       |
| Nombre            | varchar(100) | YES  |     | NULL    |       |
| CorreoElectronico | varchar(150) | YES  |     | NULL    |       |
| Ciudad            | varchar(80)  | YES  |     | NULL    |       |
| FechaRegistro     | date         | YES  |     | NULL    |       |

Aunque todavía no comprendamos todas las columnas de esta descripción, iremos interpretándolas durante los próximos capítulos.

---

### ¿Qué hemos creado realmente?

Es importante comprender que la tabla no contiene todavía información.

Lo único que hemos definido es su estructura.

Podemos imaginarla como una hoja de cálculo vacía con los encabezados ya preparados.

Más adelante comenzaremos a insertar registros utilizando las sentencias `INSERT`.

---

### Modificando la estructura

Durante el desarrollo de una aplicación es habitual que el diseño evolucione.

En lugar de eliminar y volver a crear la tabla continuamente, MySQL permite modificar su estructura mediante otras instrucciones DDL que estudiaremos más adelante.

Por el momento nos centraremos en comprender correctamente la creación inicial de las tablas.

---

### Errores frecuentes

Uno de los errores más habituales consiste en olvidar cerrar el paréntesis o separar correctamente las columnas mediante comas.

También es frecuente utilizar nombres de columnas inconsistentes o elegir tipos de datos inadecuados.

Finalmente, algunos estudiantes crean la tabla sin comprobar posteriormente su estructura mediante `DESCRIBE`, perdiendo una excelente oportunidad para detectar errores desde el principio.

### Ideas clave

* `CREATE TABLE` define la estructura física de una nueva tabla.
* Cada columna debe especificar su nombre y su tipo de dato.
* `SHOW TABLES` permite comprobar las tablas existentes.
* `DESCRIBE` muestra la estructura completa de una tabla.
* Una tabla recién creada aún no contiene registros; únicamente define cómo se almacenarán los datos.
* La tabla **Cliente** será el punto de partida del modelo físico que construiremos durante el resto del curso.

