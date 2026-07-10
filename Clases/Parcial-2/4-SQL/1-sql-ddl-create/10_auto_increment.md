# AUTO\_INCREMENT

## Introducción

Hasta ahora hemos asignado manualmente el identificador de cada cliente.

Por ejemplo:

```sql
INSERT INTO Cliente
VALUES
(
    1,
    'Ana Ruiz',
    'ana@empresa.com',
    'Santander',
    '2026-09-15',
    TRUE
);
```

Este procedimiento resulta adecuado para comprender el funcionamiento de las claves primarias, pero presenta un problema evidente.

¿Qué ocurre cuando miles de usuarios insertan registros al mismo tiempo?

¿Quién decide cuál será el siguiente identificador disponible?

La respuesta es sencilla: ​**el propio servidor MySQL**​.

Para ello existe la propiedad ​**AUTO\_INCREMENT**​, que permite generar automáticamente identificadores únicos y consecutivos.

En prácticamente todas las tablas del caso práctico utilizaremos esta característica.

---

### ¿Qué es AUTO\_INCREMENT?

`AUTO_INCREMENT` indica a MySQL que el valor de una columna debe generarse automáticamente.

Cada vez que se inserta un nuevo registro, el servidor calcula el siguiente identificador disponible.

Gracias a ello desaparece la necesidad de controlar manualmente los identificadores desde la aplicación.

---

### Modificando nuestra tabla

Volvamos a recrear la tabla `Cliente`.

```sql
DROP TABLE IF EXISTS Cliente;

CREATE TABLE Cliente (

    IdCliente INT AUTO_INCREMENT PRIMARY KEY,

    Nombre VARCHAR(100) NOT NULL,

    CorreoElectronico VARCHAR(150) NOT NULL,

    Ciudad VARCHAR(80),

    FechaRegistro DATE,

    Activo BOOLEAN DEFAULT TRUE

);
```

Ahora `IdCliente` será generado automáticamente.

---

### Insertando registros

Como el identificador ya no debe proporcionarse manualmente, simplemente omitiremos esa columna.

```sql
INSERT INTO Cliente
(
    Nombre,
    CorreoElectronico,
    Ciudad,
    FechaRegistro
)
VALUES
(
    'Ana Ruiz',
    'ana@empresa.com',
    'Santander',
    '2026-09-15'
);
```

Insertemos un segundo cliente.

```sql
INSERT INTO Cliente
(
    Nombre,
    CorreoElectronico,
    Ciudad,
    FechaRegistro
)
VALUES
(
    'Pedro López',
    'pedro@empresa.com',
    'Bilbao',
    '2026-09-20'
);
```

Consultemos ahora la tabla.

```sql
SELECT *
FROM Cliente;
```

Obtendremos un resultado similar.

| IdCliente | Nombre       |
| ----------: | -------------- |
|         1 | Ana Ruiz     |
|         2 | Pedro López |

Los identificadores han sido asignados automáticamente por MySQL.

---

### ¿Qué ocurre si eliminamos un registro?

Supongamos que eliminamos el cliente con identificador 2.

```sql
DELETE FROM Cliente
WHERE IdCliente = 2;
```

Si insertamos posteriormente un nuevo cliente:

```sql
INSERT INTO Cliente
(
    Nombre,
    CorreoElectronico
)
VALUES
(
    'Laura García',
    'laura@empresa.com'
);
```

El nuevo identificador será:

```text
3
```

MySQL **no reutiliza automáticamente** los identificadores eliminados.

Esta decisión evita numerosos problemas relacionados con la integridad referencial y la consistencia de los datos.

---

### Consultando el siguiente valor

Podemos consultar la estructura de la tabla.

```sql
SHOW CREATE TABLE Cliente;
```

Entre la información devuelta aparecerá la propiedad `AUTO_INCREMENT`, indicando el siguiente identificador que utilizará el servidor.

Aunque esta consulta genera una salida extensa, resulta muy útil para inspeccionar cómo MySQL interpreta realmente la definición de una tabla.

---

### Casos reales

En nuestro proyecto todas las entidades principales utilizarán identificadores automáticos.

Por ejemplo:

* Cliente
* Producto
* Pedido
* Factura
* Proveedor
* Empleado
* Almacén

Esta decisión simplifica el desarrollo de aplicaciones y evita conflictos cuando múltiples usuarios trabajan simultáneamente sobre la misma base de datos.

---

### Errores frecuentes

Uno de los errores más habituales consiste en seguir proporcionando manualmente el identificador después de definir `AUTO_INCREMENT`.

También es frecuente pensar que los identificadores eliminados volverán a utilizarse automáticamente, lo cual no ocurre en MySQL.

Por último, algunos estudiantes confunden un identificador consecutivo con una numeración sin huecos. En realidad, los valores generados por `AUTO_INCREMENT` únicamente garantizan la unicidad y el incremento, no la continuidad absoluta.

### Ideas clave

* `AUTO_INCREMENT` permite que MySQL genere automáticamente los identificadores.
* Habitualmente se utiliza junto con una clave primaria.
* La aplicación ya no necesita calcular el siguiente identificador disponible.
* Los identificadores eliminados no suelen reutilizarse automáticamente.
* `AUTO_INCREMENT` será la estrategia utilizada en todas las entidades principales de nuestro caso práctico.

