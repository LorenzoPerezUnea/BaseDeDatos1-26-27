# Participación total y parcial

En la clase anterior ya introdujimos el concepto de participación. Sin embargo, ahora que conocemos las distintas cardinalidades podemos estudiarlo con mayor profundidad y comprender cómo influye en el diseño del modelo.

Mientras que la **cardinalidad** responde a la pregunta:

> **¿Cuántas entidades pueden relacionarse?**

La **participación** responde a una cuestión diferente:

> **¿Es obligatorio que una entidad participe en esa relación?**

Aunque ambos conceptos aparecen juntos en los diagramas ER, describen propiedades distintas del negocio.

### Participación total

Una entidad presenta participación total cuando ​**todas sus instancias deben intervenir obligatoriamente en una relación**​.

Por ejemplo, consideremos la entidad ​**Pedido**​.

En nuestra empresa todo pedido debe haber sido realizado por un cliente.

No existe un pedido "sin propietario".

```mermaid
erDiagram

CLIENTE ||--|{ PEDIDO : realiza
```

La participación del pedido es total.

### Participación parcial

Una entidad presenta participación parcial cuando algunas de sus instancias pueden no participar en la relación.

Por ejemplo, un cliente recién registrado todavía puede no haber realizado ninguna compra.

Aun así, sigue siendo un cliente válido.

Por tanto, la participación del cliente es parcial.

### Comparando ambos conceptos

| Situación                                           | Participación |
| ------------------------------------------------------ | ---------------- |
| Todo pedido pertenece a un cliente                   | Total          |
| Un cliente puede no tener pedidos                    | Parcial        |
| Toda línea pertenece a un pedido                    | Total          |
| Un proveedor puede no suministrar todavía productos | Parcial        |

Esta información resulta muy importante durante el diseño.

### Influencia en el modelo relacional

Más adelante veremos que la participación afecta directamente a la implementación.

Por ejemplo:

* Una participación total suele implicar que la clave foránea sea obligatoria.
* Una participación parcial puede permitir valores nulos o registros sin relación.

Aunque todavía no estudiaremos estos detalles técnicos, conviene comprender que la participación no es únicamente una propiedad gráfica.

Tiene consecuencias reales sobre la base de datos.

### Caso práctico

Nuestro modelo presenta actualmente varias participaciones interesantes.

* Todo pedido pertenece a un cliente.
* Todo producto pertenece a una categoría.
* Todo empleado pertenece a un departamento (cuando incorporemos esta entidad).
* Un cliente puede existir sin pedidos.
* Un proveedor puede existir antes de suministrar productos.

Estas decisiones reflejan exactamente el funcionamiento de la empresa.

### Cómo descubrir la participación

Durante las entrevistas con el cliente suele bastar con formular preguntas muy sencillas.

Por ejemplo:

* ¿Puede existir un cliente sin pedidos?
* ¿Puede existir un pedido sin cliente?
* ¿Puede existir un producto sin categoría?
* ¿Puede existir una categoría vacía?

Las respuestas determinan automáticamente el tipo de participación.

### Ideas clave

* La participación indica si una relación es obligatoria u opcional.
* Puede ser total o parcial.
* No debe confundirse con la cardinalidad.
* Refleja reglas reales del negocio.
* Ayudará posteriormente a definir restricciones en la base de datos.

