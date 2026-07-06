# El Modelo Relacional

A finales de la década de 1960, las bases de datos existentes eran difíciles de utilizar y mantener. Los modelos jerárquico y en red permitían almacenar grandes cantidades de información, pero obligaban a los programadores a conocer con detalle cómo estaban organizados físicamente los datos.

Modificar la estructura de una base de datos podía implicar reescribir una gran parte de las aplicaciones que la utilizaban.

En 1970, el investigador Edgar F. Codd publicó un artículo que cambiaría para siempre la historia de las bases de datos: ​**"A Relational Model of Data for Large Shared Data Banks"**​.

Su propuesta introducía una idea aparentemente sencilla, pero revolucionaria: representar la información mediante ​**relaciones**​, basadas en conceptos matemáticos de la teoría de conjuntos y la lógica de predicados.

Más de cincuenta años después, esta sigue siendo la base de la mayoría de los sistemas de gestión de bases de datos.

### La idea fundamental

El Modelo Relacional propone representar la información utilizando ​**tablas**​.

Cada tabla almacena información sobre un único tipo de elemento del mundo real.

Por ejemplo:

* Clientes.
* Productos.
* Empleados.
* Pedidos.
* Facturas.

Cada tabla es independiente, pero puede relacionarse con las demás mediante claves.

Esta forma de organizar la información facilita enormemente su comprensión y mantenimiento.

### Una representación lógica

Es importante comprender que una tabla del Modelo Relacional no es simplemente una hoja de cálculo.

Aunque visualmente se parezcan, existen diferencias fundamentales.

En una hoja de cálculo podemos introducir información prácticamente en cualquier posición.

En una base de datos relacional existen reglas estrictas sobre:

* Los tipos de datos.
* Las relaciones entre tablas.
* Los valores permitidos.
* La unicidad de determinadas columnas.
* La integridad de la información.

Estas reglas garantizan que los datos permanezcan consistentes incluso cuando miles de usuarios trabajan simultáneamente.

### Independencia de los datos

Uno de los mayores logros del Modelo Relacional fue separar la forma en que los datos se almacenan físicamente de la forma en que los usuarios los consultan.

Gracias a ello, el administrador puede optimizar el almacenamiento interno sin obligar a modificar las aplicaciones.

Esta característica recibe el nombre de **independencia de los datos** y constituye uno de los principios más importantes del modelo.

### Un ejemplo sencillo

Supongamos que una empresa desea almacenar información sobre sus clientes.

Podría existir una relación como la siguiente:

| IdCliente | Nombre       | Ciudad    |
| ----------: | -------------- | ----------- |
|         1 | Ana López   | Santander |
|         2 | Carlos Ruiz  | Bilbao    |
|         3 | Marta Pérez | Oviedo    |

A simple vista parece una tabla normal.

Sin embargo, detrás de ella existen numerosas reglas que garantizan su correcto funcionamiento y que estudiaremos en los próximos capítulos.

### El papel de SQL

El Modelo Relacional define cómo deben organizarse los datos.

SQL, por el contrario, es el lenguaje que utilizaremos para trabajar con ellos.

Podemos decir que:

* El Modelo Relacional proporciona las reglas.
* SQL proporciona las herramientas para aplicar esas reglas.

Comprender esta diferencia evitará muchas confusiones en las próximas clases.

### Caso práctico

Nuestra empresa comercial almacenará la información de clientes, productos, empleados y pedidos utilizando relaciones.

Más adelante estas relaciones se convertirán en tablas de MySQL, pero antes debemos comprender qué representan realmente y qué normas deben cumplir.

### Ideas clave

* El Modelo Relacional fue propuesto por Edgar F. Codd en 1970.
* Organiza la información mediante relaciones, representadas habitualmente como tablas.
* Se basa en principios matemáticos, no únicamente en una representación gráfica.
* Separa la organización lógica de los datos de su almacenamiento físico.
* SQL es el lenguaje que permite trabajar con las bases de datos relacionales.

