# Clave primaria

## Introducción

En el capítulo anterior creamos nuestra primera tabla. Sin embargo, aunque su estructura era correcta desde el punto de vista sintáctico, presentaba un problema muy importante: ​**nada impedía que existieran dos clientes exactamente iguales**​.

Por ejemplo, podríamos insertar dos registros con el mismo identificador.

| IdCliente | Nombre       |
| ----------: | -------------- |
|         1 | Ana Ruiz     |
|         1 | Pedro López |

Esta situación genera ambigüedad. Si un pedido hace referencia al cliente con identificador ​**1**​, ¿a cuál de los dos registros corresponde?

Para resolver este problema, el modelo relacional introduce el concepto de **clave primaria** (*Primary Key* o ​**PK**​).

La clave primaria constituye uno de los elementos más importantes de una base de datos relacional y estará presente prácticamente en todas las tablas que construiremos durante el resto del curso.

---

### ¿Qué es una clave primaria?

Una clave primaria es una columna, o un conjunto de columnas, cuyos valores identifican **de forma única** cada fila de una tabla.

Esto significa que:

* no puede haber dos filas con el mismo valor;
* no puede contener valores nulos;
* cada registro posee exactamente una clave primaria.

Gracias a estas propiedades, cualquier registro puede localizarse sin ambigüedad.

En nuestro caso práctico, el atributo `IdCliente` será la clave primaria de la tabla `Cliente`.

---

### Definiendo una clave primaria

La forma más sencilla consiste en añadir la restricción al definir la columna.

Ejecute el siguiente script.

```sql
DROP TABLE IF EXISTS Cliente;

CREATE TABLE Cliente (

    IdCliente INT PRIMARY KEY,

    Nombre VARCHAR(100),

    CorreoElectronico VARCHAR(150),

    Ciudad VARCHAR(80),

    FechaRegistro DATE

);
```

Ahora `IdCliente` ha dejado de ser una columna cualquiera y se ha convertido en el identificador oficial de cada cliente.

---

### Verificando la estructura

Como en capítulos anteriores, comprobaremos el resultado.

```sql
DESC Cliente;
```

Obtendremos una salida similar a:

| Field             | Type         | Null | Key | Default | Extra |
| ------------------- | -------------- | ------ | ----- | --------- | ------- |
| IdCliente         | int          | NO   | PRI | NULL    |       |
| Nombre            | varchar(100) | YES  |     | NULL    |       |
| CorreoElectronico | varchar(150) | YES  |     | NULL    |       |
| Ciudad            | varchar(80)  | YES  |     | NULL    |       |
| FechaRegistro     | date         | YES  |     | NULL    |       |

Aparecen dos cambios importantes.

* La columna **Key** muestra el valor `PRI`.
* La columna **Null** pasa automáticamente a `NO`.

Aunque no hayamos escrito `NOT NULL`, MySQL lo aplica de forma implícita porque una clave primaria nunca puede ser nula.

---

### Intentando violar la restricción

Una buena forma de comprender una restricción consiste en intentar incumplirla.

Primero insertaremos un cliente.

```sql
INSERT INTO Cliente
VALUES
(
    1,
    'Ana Ruiz',
    'ana@empresa.com',
    'Santander',
    '2026-09-15'
);
```

Ahora intentemos insertar otro cliente utilizando el mismo identificador.

```sql
INSERT INTO Cliente
VALUES
(
    1,
    'Pedro López',
    'pedro@empresa.com',
    'Bilbao',
    '2026-09-20'
);
```

MySQL responderá con un error similar a:

```text
ERROR 1062 (23000):
Duplicate entry '1' for key 'Cliente.PRIMARY'
```

El servidor ha protegido automáticamente la integridad de los datos.

---

### Claves primarias naturales y artificiales

Existen dos estrategias muy habituales.

**Clave natural**

Utiliza un dato que ya existe en el mundo real.

Por ejemplo:

* DNI
* NIF
* ISBN
* Número de pasaporte

**Clave artificial**

Consiste en crear un identificador sin significado para el usuario.

Por ejemplo:

```text
1
2
3
4
5
...
```

En proyectos profesionales suele preferirse la segunda opción.

Durante todo este curso utilizaremos identificadores artificiales como:

* IdCliente
* IdProducto
* IdProveedor
* IdEmpleado

Esta decisión simplifica el mantenimiento del sistema y evita problemas cuando cambian los datos reales.

---

### Casos reales

Todas las tablas principales de nuestro proyecto utilizarán una clave primaria.

| Tabla     | Clave primaria |
| ----------- | ---------------- |
| Cliente   | IdCliente      |
| Producto  | IdProducto     |
| Pedido    | IdPedido       |
| Factura   | IdFactura      |
| Proveedor | IdProveedor    |

Más adelante estas claves servirán además para establecer relaciones entre tablas mediante claves foráneas.

---

### Errores frecuentes

Uno de los errores más habituales consiste en crear tablas sin clave primaria.

También es frecuente utilizar atributos que pueden cambiar con el tiempo, como el correo electrónico o el teléfono, como identificadores principales.

Finalmente, algunos estudiantes confunden la clave primaria con un índice cualquiera. Aunque toda clave primaria genera un índice, no todos los índices son claves primarias.

### Ideas clave

* Toda tabla principal debe disponer de una clave primaria.
* La clave primaria identifica de forma única cada registro.
* No admite valores duplicados ni valores nulos.
* En este curso utilizaremos identificadores artificiales para todas las entidades principales.
* La clave primaria será la base para construir posteriormente las relaciones entre tablas.

