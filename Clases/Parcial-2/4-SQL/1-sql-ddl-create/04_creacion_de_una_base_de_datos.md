# Creación de una base de datos

## Introducción

En las clases anteriores hemos trabajado con modelos conceptuales, esquemas relacionales y expresiones en Álgebra Relacional. Sin embargo, hasta este momento la base de datos solo existía como un diseño sobre el papel.

Ha llegado el momento de crearla realmente.

Toda base de datos relacional debe existir primero como un objeto dentro del Sistema Gestor de Bases de Datos. Ese objeto actuará como un contenedor donde posteriormente almacenaremos tablas, vistas, índices, procedimientos almacenados y el resto de elementos que formarán parte del sistema.

En MySQL este contenedor recibe el nombre de **base de datos** (*database* o ​*schema*​, dependiendo del contexto). Durante el resto del curso utilizaremos una única base de datos denominada ​**empresa\_tecnologica**​, que irá creciendo progresivamente conforme incorporemos nuevas tablas y funcionalidades.

En este capítulo realizaremos nuestra primera interacción real con MySQL.

---

### Comprobando el estado inicial

Una vez iniciado el servidor mediante Docker y establecida la conexión desde MySQL Workbench o phpMyAdmin, podemos consultar las bases de datos existentes.

Ejecutaremos la siguiente sentencia:

```sql
SHOW DATABASES;
```

El resultado será similar al siguiente.

| Database                               |
| ---------------------------------------- |
| information\_schema                    |
| mysql                                  |
| performance\_schema                    |
| sys                                    |
| empresa\_tecnologica*(si ya existe)* |

Las primeras bases de datos pertenecen al propio sistema gestor y contienen información interna utilizada por MySQL para administrar usuarios, permisos, estadísticas y configuración.

Como desarrolladores, normalmente trabajaremos únicamente con las bases de datos creadas para nuestras aplicaciones.

---

### Nuestra primera sentencia DDL

Vamos a crear la base de datos del caso práctico.

```sql
CREATE DATABASE empresa_tecnologica;
```

Si la instrucción se ejecuta correctamente, MySQL responderá con un mensaje similar a:

```text
Query OK, 1 row affected
```

Aunque el mensaje indique "1 row affected", no se ha insertado ningún registro.

Simplemente se ha creado un nuevo objeto dentro del servidor.

A partir de este momento ya disponemos de un espacio donde construiremos toda la estructura de la empresa comercial.

---

### Verificando el resultado

Una buena práctica consiste en comprobar siempre que una operación ha producido el efecto esperado.

Volvamos a ejecutar:

```sql
SHOW DATABASES;
```

Ahora debería aparecer nuestra nueva base de datos.

Este pequeño hábito de verificar cada cambio será muy importante durante todo el curso y ayudará a detectar errores mucho antes de que se propaguen al resto del proyecto.

---

### Seleccionando la base de datos activa

Crear una base de datos no significa que vayamos a trabajar automáticamente sobre ella.

Debemos indicar explícitamente cuál será la base de datos activa de la sesión.

Para ello utilizamos la instrucción:

```sql
USE empresa_tecnologica;
```

A partir de ese momento, todas las tablas que creemos pertenecerán a esta base de datos.

Si olvidamos ejecutar esta instrucción, MySQL normalmente responderá con errores cuando intentemos crear tablas o insertar registros.

---

### Comprobando el contexto de trabajo

Podemos verificar cuál es la base de datos actualmente seleccionada mediante:

```sql
SELECT DATABASE();
```

El resultado será:

| DATABASE()           |
| ---------------------- |
| empresa\_tecnologica |

Esta consulta resulta especialmente útil cuando trabajamos con varios proyectos simultáneamente y queremos asegurarnos de que estamos modificando la base de datos correcta.

---

### Evitando errores al crear la base de datos

Si intentamos ejecutar nuevamente:

```sql
CREATE DATABASE empresa_tecnologica;
```

MySQL responderá con un error indicando que la base de datos ya existe.

Para evitar este problema podemos utilizar una variante mucho más segura:

```sql
CREATE DATABASE IF NOT EXISTS empresa_tecnologica;
```

Esta instrucción crea la base de datos únicamente si todavía no existe.

En caso contrario, simplemente continúa la ejecución sin producir un error.

Durante este curso adoptaremos esta variante como buena práctica en la mayoría de nuestros scripts de inicialización.

---

### Nuestro primer script SQL

A partir de esta clase comenzaremos a organizar el código en pequeños scripts reutilizables.

Por ejemplo, el primer script de creación podría escribirse así:

```sql
CREATE DATABASE IF NOT EXISTS empresa_tecnologica;

USE empresa_tecnologica;
```

Este archivo podrá ejecutarse tantas veces como sea necesario al iniciar un nuevo entorno de trabajo.

En las próximas clases iremos ampliándolo con la creación de tablas, restricciones y datos de prueba, hasta convertirlo en el script completo de inicialización de nuestra base de datos.

---

### Errores frecuentes

Uno de los errores más habituales consiste en olvidar ejecutar la sentencia `USE`, provocando que las tablas se creen en otra base de datos o que MySQL muestre un mensaje indicando que no se ha seleccionado ningún esquema.

También es frecuente intentar crear varias veces la misma base de datos sin utilizar `IF NOT EXISTS`, lo que interrumpe innecesariamente la ejecución del script.

Por último, muchos principiantes ejecutan sentencias sin comprobar el resultado. Acostumbrarse a utilizar consultas de verificación como `SHOW DATABASES` o `SELECT DATABASE()` facilita enormemente la detección temprana de errores.

### Ideas clave

* Una base de datos es el contenedor donde se almacenarán todos los objetos del proyecto.
* `CREATE DATABASE` crea una nueva base de datos dentro del servidor MySQL.
* `SHOW DATABASES` permite verificar las bases de datos existentes.
* `USE` selecciona la base de datos activa para la sesión actual.
* `SELECT DATABASE()` permite comprobar sobre qué base de datos estamos trabajando.
* La cláusula `IF NOT EXISTS` hace que los scripts sean más robustos y reutilizables.
* A partir de esta clase construiremos progresivamente la base de datos ​**empresa\_tecnologica**​, reutilizando siempre el mismo esquema durante todo el curso.

