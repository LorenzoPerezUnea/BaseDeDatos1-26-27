# Entidades fuertes a tablas

La primera regla de transformación es también la más sencilla y la más importante de todo el proceso.

> **Toda entidad fuerte del Modelo Entidad-Relación se transforma en una tabla del Modelo Relacional.**

Esta regla será aplicada una y otra vez durante el resto del curso.

### ¿Qué es una entidad fuerte?

Recordemos que una entidad fuerte es aquella que:

* Existe por sí misma.
* Posee un identificador propio.
* No depende de otra entidad para ser identificada.

Ejemplos de nuestro caso de estudio son:

* Cliente
* Producto
* Pedido
* Categoría
* Empleado
* Proveedor

Todas ellas cumplen esta condición.

### Primera transformación

Supongamos que partimos del siguiente fragmento del modelo ER.

```mermaid
erDiagram

CLIENTE
```

La transformación inmediata será:

```text
CLIENTE

-------------------------
IdCliente
Nombre
Telefono
Correo
```

La entidad ha desaparecido.

Ahora tenemos una tabla.

### Un ejemplo completo

Consideremos tres entidades del modelo conceptual.

```mermaid
erDiagram

CLIENTE

PRODUCTO

PEDIDO
```

Tras aplicar la transformación obtenemos:

```text
CLIENTE
-------------------------
IdCliente
Nombre
Telefono
Correo

PRODUCTO
-------------------------
IdProducto
Nombre
Precio
Stock

PEDIDO
-------------------------
IdPedido
Fecha
Estado
```

Todavía no existen relaciones.

Simplemente hemos convertido entidades en tablas.

### Una tabla representa un conjunto

Es importante comprender que una tabla no representa un único cliente.

Representa ​**todos los clientes**​.

Cada fila corresponderá posteriormente a una instancia concreta.

Por ejemplo:

| IdCliente | Nombre       |
| ----------: | -------------- |
|         1 | Ana López   |
|         2 | Carlos Ruiz  |
|         3 | Marta Gómez |

La tabla describe el conjunto completo.

### El nombre de la tabla

Existen varias convenciones.

Algunas organizaciones utilizan nombres en singular.

```text
Cliente
Producto
Pedido
```

Otras prefieren el plural.

```text
Clientes
Productos
Pedidos
```

Lo importante es mantener la misma convención durante todo el proyecto.

En este curso utilizaremos ​**el singular**​, ya que coincide con la representación utilizada en el Modelo ER.

### Nuestro caso práctico

La primera versión del Modelo Relacional de la empresa comercial contendrá inicialmente las siguientes tablas.

```text
CLIENTE

PRODUCTO

PEDIDO

EMPLEADO

PROVEEDOR

CATEGORIA
```

Más adelante aparecerán nuevas tablas como:

* Factura
* LíneaPedido
* Pago
* Inventario

### Ideas clave

* Toda entidad fuerte se convierte en una tabla.
* Cada tabla representa un conjunto de instancias.
* El identificador de la entidad pasará posteriormente a convertirse en la clave primaria.
* Esta transformación no modifica el significado del modelo.
* Es la regla más sencilla y más utilizada de todo el proceso.

