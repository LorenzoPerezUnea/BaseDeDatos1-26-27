# Transformación de atributos

Ya sabemos transformar entidades fuertes y débiles en tablas.

El siguiente paso consiste en convertir sus atributos.

La regla general es extremadamente sencilla.

> **Cada atributo del Modelo Entidad-Relación se convierte en una columna de la tabla correspondiente.**

Aunque parezca una transformación trivial, más adelante veremos que algunos tipos especiales de atributos requieren tratamientos diferentes.

### La transformación básica

Supongamos la siguiente entidad.

```text
CLIENTE

IdCliente
Nombre
Telefono
Correo
FechaAlta
```

Su equivalente relacional será:

```text
CLIENTE

----------------------------------------
IdCliente
Nombre
Telefono
Correo
FechaAlta
```

Los atributos simplemente pasan a convertirse en columnas.

### Correspondencia

La relación entre ambos modelos puede resumirse en la siguiente tabla.

| Modelo ER | Modelo Relacional |
| ----------- | ------------------- |
| Entidad   | Tabla             |
| Atributo  | Columna           |

Es probablemente la transformación más directa de todo el proceso.

### El orden de las columnas

Desde un punto de vista lógico, el orden de las columnas no modifica el funcionamiento de la base de datos.

Sin embargo, por claridad suele seguirse una convención.

Primero se coloca la clave primaria.

Después los atributos más importantes.

Finalmente los atributos secundarios.

Por ejemplo:

```text
CLIENTE

IdCliente

Nombre

Apellidos

Telefono

Correo

FechaAlta
```

Esta organización facilita la lectura del modelo.

### ¿Todos los atributos se transforman igual?

Todavía no.

En las próximas secciones estudiaremos casos especiales como:

* atributos multivaluados;
* atributos compuestos;
* atributos derivados.

Estos requieren reglas específicas.

### Caso práctico

Las principales tablas de nuestra empresa comenzarán a adoptar el siguiente aspecto.

```text
CLIENTE

IdCliente
Nombre
Apellidos
Telefono
Correo

PRODUCTO

IdProducto
Nombre
Precio
Stock

PEDIDO

IdPedido
Fecha
Estado
```

En las siguientes lecciones incorporaremos claves primarias, claves foráneas y restricciones.

### Ideas clave

* Cada atributo se transforma normalmente en una columna.
* La transformación es directa y sencilla.
* Conviene seguir una organización coherente de las columnas.
* Algunos tipos especiales de atributos requieren reglas particulares.
* Esta transformación acerca el modelo conceptual a su implementación definitiva.

