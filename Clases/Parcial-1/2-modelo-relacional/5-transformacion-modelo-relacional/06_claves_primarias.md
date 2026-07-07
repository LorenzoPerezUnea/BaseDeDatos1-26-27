# Claves primarias

Hasta ahora hemos transformado entidades en tablas y atributos en columnas.

Sin embargo, todavía existe un problema importante.

¿Cómo distinguimos un registro de todos los demás?

Imaginemos una tabla con miles de clientes.

¿Cómo podemos identificar exactamente a uno de ellos?

La respuesta es mediante una ​**clave primaria**​.

La clave primaria es uno de los conceptos más importantes de todo el Modelo Relacional.

### ¿Qué es una clave primaria?

Una clave primaria (Primary Key o ​**PK**​) es un atributo —o un conjunto de atributos— que identifica de forma única cada fila de una tabla.

Ningún registro puede compartir el mismo valor de la clave primaria.

Por ejemplo:

| IdCliente | Nombre       |
| ----------: | -------------- |
|         1 | Ana López   |
|         2 | Carlos Ruiz  |
|         3 | Laura Pérez |

Aunque dos clientes pudieran llamarse igual, nunca compartirán el mismo ​**IdCliente**​.

### Del identificador a la clave primaria

En el Modelo ER hablábamos de ​**identificadores**​.

Durante la transformación al Modelo Relacional esos identificadores pasan a convertirse en claves primarias.

```text
Modelo ER

Identificador

↓

Modelo Relacional

PRIMARY KEY
```

No estamos creando una nueva información.

Simplemente estamos representando la misma idea utilizando el lenguaje del Modelo Relacional.

### Propiedades de una clave primaria

Una buena clave primaria debe cumplir varias características.

* Debe identificar una única fila.
* No puede repetirse.
* No puede contener valores nulos.
* Debe permanecer estable durante toda la vida del registro.

Estas propiedades garantizan la integridad de la información.

### Claves naturales y artificiales

Existen dos estrategias principales para elegir una clave primaria.

#### Clave natural

Utiliza un dato que ya existe en el negocio.

Ejemplos:

* DNI.
* ISBN.
* Número de bastidor.
* Código EAN.

Ventajas:

* Ya existe.
* Tiene significado para los usuarios.

Inconvenientes:

* Puede cambiar.
* Depende de normas externas.
* A veces resulta demasiado largo.

#### Clave artificial

Se crea únicamente para identificar registros.

Ejemplos:

```text
IdCliente

IdProducto

IdPedido
```

Ventajas:

* Nunca cambia.
* Es sencilla.
* Facilita las relaciones entre tablas.

Por este motivo, la mayoría de aplicaciones modernas utilizan identificadores artificiales.

### Claves compuestas

En algunos casos una única columna no basta para identificar un registro.

Por ejemplo:

```text
LINEAPEDIDO

IdPedido

NumeroLinea
```

La combinación de ambas columnas identifica una línea concreta.

Esto recibe el nombre de ​**clave primaria compuesta**​.

### Caso práctico

Nuestro modelo utilizará inicialmente claves artificiales para casi todas las tablas.

| Tabla      | Clave primaria |
| ------------ | ---------------- |
| Cliente    | IdCliente      |
| Producto   | IdProducto     |
| Pedido     | IdPedido       |
| Categoría | IdCategoria    |
| Empleado   | IdEmpleado     |
| Proveedor  | IdProveedor    |

Más adelante veremos cómo MySQL implementa estas claves mediante la restricción `PRIMARY KEY`.

### Ideas clave

* La clave primaria identifica de forma única cada fila.
* Procede directamente del identificador del Modelo ER.
* No admite duplicados ni valores nulos.
* Puede ser simple o compuesta.
* En la mayoría de aplicaciones se utilizan identificadores artificiales.

