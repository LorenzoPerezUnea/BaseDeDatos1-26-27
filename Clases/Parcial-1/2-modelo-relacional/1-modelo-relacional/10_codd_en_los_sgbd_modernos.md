# Codd en los SGBD modernos

Han pasado más de cincuenta años desde la publicación del Modelo Relacional y más de cuarenta desde la formulación de las reglas de Codd.

Durante este tiempo la informática ha evolucionado enormemente. Han aparecido nuevos tipos de bases de datos, arquitecturas distribuidas, servicios en la nube y sistemas capaces de almacenar volúmenes masivos de información.

A pesar de estos cambios, las ideas fundamentales de Codd siguen presentes en la mayoría de los Sistemas Gestores de Bases de Datos Relacionales.

### ¿Cumplen los SGBD actuales todas las reglas?

La respuesta es **no**.

Ningún producto comercial cumple de manera perfecta las doce reglas.

Esto no significa que no sean relacionales.

Muchas reglas representan ideales teóricos difíciles de alcanzar completamente o cuya implementación supondría importantes pérdidas de rendimiento.

En consecuencia, los fabricantes realizan determinados compromisos entre pureza teórica y eficiencia práctica.

### Ejemplos en MySQL

A lo largo del curso utilizaremos MySQL.

Este gestor incorpora gran parte de las ideas del Modelo Relacional:

* Organización mediante tablas.
* Claves primarias.
* Claves foráneas.
* Restricciones de integridad.
* Lenguaje SQL.
* Vistas.
* Transacciones (con InnoDB).
* Catálogo del sistema.

Sin embargo, también presenta algunas diferencias respecto al modelo teórico.

Por ejemplo, determinadas operaciones permiten comportamientos que Codd probablemente habría considerado poco deseables, especialmente cuando se utilizan configuraciones heredadas o motores de almacenamiento antiguos.

### Otros gestores relacionales

La mayoría de los grandes SGBD siguen la misma filosofía.

Entre ellos encontramos:

* PostgreSQL
* Oracle Database
* Microsoft SQL Server
* MariaDB

Todos ellos implementan los principios esenciales del Modelo Relacional, aunque con pequeñas diferencias en la sintaxis SQL y en determinadas funcionalidades.

### ¿Siguen siendo importantes las reglas?

Sí.

Aunque muchos desarrolladores nunca las hayan leído, las reglas de Codd continúan influyendo en el diseño de:

* Lenguajes SQL.
* Restricciones de integridad.
* Motores de almacenamiento.
* Sistemas de optimización de consultas.
* Herramientas de administración.

Comprender estas ideas facilita interpretar por qué los SGBD funcionan como lo hacen.

### Caso práctico

Durante este curso utilizaremos MySQL para implementar la base de datos de nuestra empresa comercial.

Aunque no estudiaremos todas las diferencias entre gestores, los conceptos aprendidos serán fácilmente transferibles a PostgreSQL, SQL Server, Oracle o MariaDB.

Esa es precisamente una de las mayores ventajas del Modelo Relacional: sus principios son comunes a todos ellos.

### Ideas clave

* Las reglas de Codd siguen siendo la referencia teórica del Modelo Relacional.
* Ningún SGBD comercial las cumple de forma absoluta.
* MySQL implementa la mayoría de los principios fundamentales.
* Los conocimientos adquiridos durante el curso serán aplicables a otros gestores relacionales.
* Comprender el Modelo Relacional facilita aprender cualquier SGBD moderno.
