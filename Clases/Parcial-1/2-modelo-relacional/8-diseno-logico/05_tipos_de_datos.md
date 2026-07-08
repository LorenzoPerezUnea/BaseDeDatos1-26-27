# Tipos de datos

Una vez definidas las tablas y sus columnas, debemos decidir ​**qué tipo de información almacenará cada una**​.

Esta decisión es mucho más importante de lo que parece.

Elegir correctamente los tipos de datos influye en:

* el espacio ocupado por la base de datos;
* el rendimiento de las consultas;
* la validación de la información;
* la integridad de los datos.

### ¿Qué es un tipo de dato?

Un tipo de dato define:

* qué valores puede almacenar una columna;
* cuánto espacio ocupará;
* qué operaciones podrán realizarse sobre ella.

Por ejemplo, un precio y una fecha son conceptos completamente distintos.

No deberían almacenarse utilizando el mismo tipo de dato.

### Algunos ejemplos

En nuestro caso práctico podríamos encontrar columnas como las siguientes.

| Columna     | Tipo esperado   |
| ------------- | ----------------- |
| IdCliente   | Entero          |
| Nombre      | Texto           |
| Precio      | Número decimal |
| FechaPedido | Fecha           |
| Activo      | Valor lógico   |

Cada atributo debe utilizar el tipo que mejor represente su significado.

### Elegir el tipo más específico

Una buena práctica consiste en seleccionar el tipo más preciso posible.

Por ejemplo, si una columna almacena únicamente fechas, no tiene sentido utilizar un tipo de texto.

Del mismo modo, un precio no debería almacenarse como una cadena de caracteres.

Cuanto más específico sea el tipo, mayor será la capacidad del sistema para validar la información.

### Evitar tipos excesivamente grandes

También es importante evitar tipos sobredimensionados.

Por ejemplo, si sabemos que un código interno nunca superará diez caracteres, no resulta razonable reservar espacio para miles de ellos.

Elegir tamaños adecuados mejora el aprovechamiento del almacenamiento y puede incrementar el rendimiento.

### Pensando en MySQL

En la siguiente parte del curso conoceremos los tipos de datos concretos que ofrece MySQL, como:

* `INT`
* `BIGINT`
* `VARCHAR`
* `DATE`
* `DATETIME`
* `DECIMAL`
* `BOOLEAN`

Por el momento basta con comprender que cada atributo debe utilizar el tipo que mejor represente la naturaleza de sus datos.

### Ideas clave

* El tipo de dato determina cómo se almacena la información.
* Elegir un tipo adecuado mejora la integridad y el rendimiento.
* Cada atributo debe utilizar el tipo más específico posible.
* Deben evitarse tipos innecesariamente grandes.
* En las próximas clases estudiaremos los tipos concretos disponibles en MySQL.

