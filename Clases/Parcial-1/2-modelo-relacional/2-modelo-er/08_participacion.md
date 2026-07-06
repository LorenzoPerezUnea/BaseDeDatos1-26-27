# Participación

Conocer que dos entidades están relacionadas no siempre es suficiente.

También debemos responder otra pregunta importante:

**¿Es obligatorio que todas las entidades participen en esa relación?**

La respuesta nos conduce al concepto de ​**participación**​.

La participación indica si la presencia de una entidad en una relación es obligatoria u opcional.

### Participación total

Una entidad presenta participación total cuando **todas sus instancias deben participar obligatoriamente** en una determinada relación.

Por ejemplo, imaginemos la entidad ​**LíneaPedido**​.

Cada línea pertenece necesariamente a un pedido.

No puede existir una línea aislada.

Por tanto, su participación es total.

```mermaid
flowchart LR

Pedido --> LineaPedido
```

### Participación parcial

La participación es parcial cuando algunas instancias pueden no intervenir en la relación.

Por ejemplo:

Un cliente recién registrado puede no haber realizado todavía ningún pedido.

Sin embargo, sigue siendo un cliente válido.

En consecuencia:

* Cliente → participación parcial.
* Pedido → participación total.

Todo pedido pertenece a un cliente.

Pero no todo cliente tiene necesariamente un pedido.

### Ejemplo práctico

Supongamos que nuestra empresa acaba de incorporar un nuevo proveedor.

Todavía no suministra ningún producto.

¿Debe aparecer en la base de datos?

Sí.

Eso significa que la participación del proveedor respecto al suministro de productos es parcial.

### ¿Por qué es importante?

La participación ayuda a definir correctamente las reglas del negocio.

Más adelante determinará:

* Qué relaciones son obligatorias.
* Qué claves foráneas podrán admitir valores nulos.
* Qué restricciones deberán aplicarse durante la implementación.

Por ello resulta fundamental comprenderla antes de diseñar el modelo relacional.

### Caso práctico

En nuestra empresa comercial encontramos varios ejemplos.

| Relación              | Participación |
| ------------------------ | ---------------- |
| Pedido → Cliente      | Total          |
| Cliente → Pedido      | Parcial        |
| LíneaPedido → Pedido | Total          |
| Producto → Categoría | Total          |
| Categoría → Producto | Parcial        |

Estas decisiones reflejan el funcionamiento real del negocio.

### Errores frecuentes

Es habitual confundir participación con cardinalidad.

Aunque ambos conceptos están relacionados, responden a preguntas distintas.

La **cardinalidad** responde a:

> ¿Cuántas instancias pueden relacionarse?

La **participación** responde a:

> ¿Es obligatorio participar en la relación?

Ambos conceptos deben analizarse por separado.

### Ideas clave

* La participación indica si una relación es obligatoria u opcional para una entidad.
* Puede ser total o parcial.
* No debe confundirse con la cardinalidad.
* Refleja reglas reales del negocio.
* Será fundamental cuando transformemos el modelo conceptual en un modelo relacional.

