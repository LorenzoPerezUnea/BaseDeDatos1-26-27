# Entidades fuertes y débiles

Hasta este momento hemos considerado que todas las entidades pueden existir de manera independiente. Sin embargo, en muchos sistemas aparecen entidades cuya existencia depende necesariamente de otra.

Esta diferencia da lugar a una clasificación muy importante dentro del Modelo Entidad-Relación: las **entidades fuertes** y las ​**entidades débiles**​.

Comprender esta distinción resulta fundamental para diseñar correctamente determinadas relaciones y evitar errores durante la transformación al Modelo Relacional.

### Entidades fuertes

Una entidad fuerte es aquella que puede identificarse por sí misma.

Posee un identificador propio y no necesita depender de otra entidad para existir.

Por ejemplo, en nuestra empresa comercial:

* Cliente
* Producto
* Empleado
* Proveedor

Cada uno puede existir independientemente de los demás.

Podemos registrar un nuevo cliente aunque todavía no haya realizado ningún pedido.

Del mismo modo, un producto puede existir en el catálogo aunque todavía no se haya vendido.

### Entidades débiles

Una entidad débil no puede identificarse completamente por sí misma.

Necesita apoyarse en otra entidad para adquirir significado.

Su existencia depende de una entidad fuerte.

Un ejemplo clásico es el de las ​**líneas de un pedido**​.

Supongamos el siguiente pedido.

```text
Pedido 105

- 2 Monitores
- 1 Teclado
- 3 Ratones
```

Cada línea únicamente tiene sentido dentro de ese pedido.

Si eliminamos el pedido, las líneas dejan de tener significado.

No tendría sentido conservarlas aisladas.

### Dependencia de existencia

La principal característica de una entidad débil es la ​**dependencia de existencia**​.

Esto significa que:

* Si desaparece la entidad fuerte, también desaparece la entidad débil.
* La entidad débil no puede crearse sin que exista previamente la fuerte.

En nuestro ejemplo:

```mermaid
flowchart LR

Pedido --> LineaPedido
```

La existencia de una línea depende completamente del pedido al que pertenece.

### Identificación

Habitualmente una entidad débil necesita combinar:

* El identificador de la entidad fuerte.
* Un identificador parcial propio.

Por ejemplo:

| Pedido | Nº Línea | Producto |
| -------- | ------------ | ---------- |
| 105    | 1          | Monitor  |
| 105    | 2          | Ratón   |
| 105    | 3          | Teclado  |

El número de línea por sí solo no identifica nada.

Debe combinarse con el pedido correspondiente.

### Representación clásica

En la notación de Chen:

* Las entidades fuertes se representan mediante un rectángulo simple.
* Las entidades débiles mediante un rectángulo doble.

Durante este curso utilizaremos diagramas simplificados, pero seguiremos distinguiendo ambos conceptos.

### Caso práctico

En nuestro sistema consideraremos inicialmente como entidades fuertes:

* Cliente
* Producto
* Empleado
* Proveedor
* Pedido
* Factura

Más adelante aparecerán entidades débiles como:

* LíneaPedido
* LíneaFactura

Estas solo existirán asociadas a un documento principal.

### Errores frecuentes

Es habitual que los principiantes conviertan cualquier tabla secundaria en una entidad débil.

Sin embargo, una entidad no es débil porque tenga pocos atributos.

Lo es únicamente cuando ​**su existencia depende de otra entidad**​.

### Ideas clave

* Una entidad fuerte posee identidad propia.
* Una entidad débil depende de otra para existir.
* La dependencia afecta tanto a la existencia como a la identificación.
* Las líneas de pedido constituyen uno de los ejemplos más habituales de entidad débil.
* Distinguir correctamente ambos tipos facilitará el diseño del modelo relacional.

