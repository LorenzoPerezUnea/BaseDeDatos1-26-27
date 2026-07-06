# Relaciones

Hasta ahora hemos identificado los objetos importantes de nuestro sistema.

Sin embargo, una empresa no es simplemente una colección de clientes, productos y empleados independientes.

Todos ellos interactúan continuamente.

Los clientes realizan pedidos.

Los empleados gestionan ventas.

Los proveedores suministran productos.

Estas conexiones reciben el nombre de ​**relaciones**​.

Las relaciones son el elemento que convierte un conjunto de entidades aisladas en un verdadero modelo de datos.

### ¿Qué es una relación?

Una relación representa una asociación lógica entre dos o más entidades.

Describe cómo interactúan entre sí los distintos elementos del sistema.

Por ejemplo:

* Un cliente realiza pedidos.
* Un pedido contiene productos.
* Un proveedor suministra productos.
* Un empleado tramita pedidos.

Estas frases expresan relaciones.

### Identificar relaciones

Una técnica muy útil consiste en buscar los **verbos** del enunciado.

Si analizamos el texto:

> "Los clientes realizan pedidos que contienen productos."

Encontramos los verbos:

* realizan
* contienen

Cada verbo representa un posible candidato a relación.

### Relaciones binarias

Las relaciones más habituales conectan dos entidades.

Por ejemplo:

```mermaid
flowchart LR

Cliente --- Pedido
```

o bien:

```mermaid
flowchart LR

Proveedor --- Producto
```

Este tipo recibe el nombre de ​**relación binaria**​.

La inmensa mayoría de las relaciones de una base de datos pertenecen a esta categoría.

### Cardinalidad

Además de saber que dos entidades están relacionadas, también debemos conocer ​**cuántas instancias pueden participar**​.

Las cardinalidades más habituales son:

| Cardinalidad | Significado     |
| -------------- | ----------------- |
| 1 : 1        | Uno a uno       |
| 1 : N        | Uno a muchos    |
| N : M        | Muchos a muchos |

Estos conceptos serán estudiados con mucho más detalle en las próximas clases, pero conviene conocerlos desde ahora.

### Ejemplos

#### Uno a uno

Cada empleado dispone de un único despacho.

Cada despacho pertenece a un único empleado.

#### Uno a muchos

Un cliente puede realizar muchos pedidos.

Cada pedido pertenece únicamente a un cliente.

#### Muchos a muchos

Un pedido contiene muchos productos.

Un mismo producto puede aparecer en muchos pedidos.

Esta última situación suele resolverse posteriormente mediante una entidad intermedia.

### Representación

En un diagrama ER las relaciones se representan mediante líneas que unen entidades.

```mermaid
erDiagram

CLIENTE ||--o{ PEDIDO : realiza
```

Más adelante utilizaremos esta notación de forma habitual.

### Caso práctico

Nuestro modelo inicial incluirá relaciones como:

* Cliente realiza Pedido.
* Empleado gestiona Pedido.
* Pedido contiene Producto.
* Proveedor suministra Producto.
* Producto pertenece a Categoría.

Estas relaciones irán ampliándose durante el semestre.

### Ideas clave

* Una relación conecta dos o más entidades.
* Los verbos del enunciado ayudan a descubrir relaciones.
* Las relaciones describen cómo interactúan las entidades.
* Las relaciones poseen cardinalidades.
* Sin relaciones no existiría un modelo de datos coherente.

