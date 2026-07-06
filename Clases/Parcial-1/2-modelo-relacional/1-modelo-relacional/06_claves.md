# Claves

A medida que una base de datos crece, aumenta también el número de registros almacenados. Una empresa puede tener miles de clientes, decenas de miles de productos y millones de pedidos.

En estas circunstancias surge una pregunta fundamental:

**¿Cómo distinguimos un registro de todos los demás?**

La respuesta la proporciona uno de los conceptos más importantes del Modelo Relacional: ​**las claves**​.

Las claves permiten identificar registros, evitar duplicados y establecer relaciones entre distintas tablas. Sin ellas, una base de datos relacional perdería gran parte de su utilidad.

### ¿Qué es una clave?

Una clave es un atributo, o un conjunto de atributos, cuyos valores permiten identificar una tupla de forma única dentro de una relación.

Esto significa que no pueden existir dos registros con el mismo valor para esa clave.

Por ejemplo, si una empresa asigna un identificador único a cada cliente, dicho identificador puede utilizarse como clave.

| IdCliente | Nombre      | Ciudad    |
| ----------: | ------------- | ----------- |
|         1 | Ana López  | Santander |
|         2 | Carlos Ruiz | Bilbao    |
|         3 | Ana López  | Santander |

Observemos que pueden existir dos personas con el mismo nombre y viviendo en la misma ciudad.

Sin embargo, nunca deberían compartir el mismo ​**IdCliente**​.

### ¿Por qué no utilizar el nombre?

Una duda frecuente consiste en preguntarse por qué no utilizar directamente el nombre de una persona como identificador.

La respuesta es sencilla.

Muchas personas pueden llamarse igual.

Además:

* Los nombres pueden escribirse incorrectamente.
* Algunas personas cambian de apellido.
* Existen nombres muy largos.
* Puede haber diferencias de mayúsculas, acentos o abreviaturas.

Un identificador numérico evita todos estos problemas.

### Tipos de claves

El Modelo Relacional distingue varios tipos de claves.

Aunque más adelante profundizaremos en ellas, conviene conocer las más importantes.

| Tipo de clave                | Función                                                                            |
| ------------------------------ | ------------------------------------------------------------------------------------- |
| Superclave                   | Identifica de forma única una tupla, aunque pueda contener atributos innecesarios. |
| Clave candidata              | Identifica una tupla utilizando únicamente los atributos necesarios.               |
| Clave primaria (Primary Key) | Clave candidata elegida para identificar oficialmente cada registro.                |
| Clave alternativa            | Clave candidata que no fue elegida como primaria.                                   |
| Clave foránea (Foreign Key) | Permite relacionar una tabla con otra.                                              |

Durante las primeras prácticas trabajaremos principalmente con claves primarias y claves foráneas.

### Clave primaria

La clave primaria posee dos características fundamentales:

* Debe identificar de forma única cada registro.
* No puede contener valores nulos.

Por ejemplo:

| **IdProducto** | Nombre  | Precio |
| ---------------------: | --------- | -------: |
|                  101 | Ratón  |  18,50 |
|                  102 | Teclado |  42,90 |
|                  103 | Monitor | 199,00 |

En este caso, **IdProducto** es la clave primaria.

### Clave foránea

Una clave foránea permite conectar dos relaciones.

Supongamos las siguientes tablas:

**Clientes**

| IdCliente | Nombre |
| ----------: | -------- |
|         1 | Ana    |
|         2 | Carlos |

**Pedidos**

| IdPedido | IdCliente | Fecha      |
| ---------: | ----------: | ------------ |
|       10 |         1 | 2026-09-03 |
|       11 |         2 | 2026-09-04 |

La columna **IdCliente** de la tabla **Pedidos** hace referencia a la clave primaria de la tabla ​**Clientes**​.

Gracias a ello sabemos qué cliente realizó cada pedido.

### Caso práctico

Nuestra empresa utilizará identificadores numéricos para todas las entidades principales:

* Clientes
* Productos
* Empleados
* Pedidos
* Facturas
* Proveedores

Estos identificadores facilitarán las relaciones entre tablas y evitarán problemas derivados de nombres repetidos.

### Errores frecuentes

Uno de los errores más habituales consiste en elegir como clave primaria un dato que puede cambiar con el tiempo.

Por ejemplo:

* Número de teléfono.
* Correo electrónico.
* Matrícula de un vehículo.
* Nombre de usuario.

Aunque puedan ser únicos en un momento determinado, todos ellos pueden modificarse.

Por ello suele preferirse un identificador interno generado por la propia base de datos.

### Ideas clave

* Las claves permiten identificar registros de forma única.
* La clave primaria identifica oficialmente cada tupla.
* Una clave primaria nunca puede repetirse ni contener valores nulos.
* Las claves foráneas permiten relacionar distintas tablas.
* Un buen diseño de claves facilita enormemente el funcionamiento de una base de datos.

