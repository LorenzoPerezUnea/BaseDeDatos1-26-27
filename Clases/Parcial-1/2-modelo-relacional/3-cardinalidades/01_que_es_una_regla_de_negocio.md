# ¿Qué es una regla de negocio?

Cuando una empresa decide desarrollar una base de datos, no basta con conocer qué información desea almacenar. También es necesario comprender ​**cómo funciona realmente el negocio**​.

Las empresas no operan de forma aleatoria. Existen normas, procedimientos y restricciones que determinan qué situaciones son válidas y cuáles no.

Estas normas reciben el nombre de ​**reglas de negocio**​.

Las reglas de negocio constituyen uno de los elementos más importantes durante el análisis de requisitos, ya que condicionan directamente el diseño de la base de datos y de la aplicación.

### Una definición intuitiva

Una regla de negocio es una condición que debe cumplirse para que el sistema represente correctamente la realidad de la organización.

No es una limitación técnica de MySQL ni una decisión del programador.

Es una norma impuesta por el funcionamiento del propio negocio.

Por ejemplo:

* Todo pedido debe pertenecer a un cliente.
* Un producto debe tener un precio mayor que cero.
* Un empleado solo puede pertenecer a un departamento.
* Una factura debe corresponder a un pedido existente.

Estas reglas existirían incluso aunque la empresa trabajara con documentos en papel.

### ¿Por qué son importantes?

Las reglas de negocio permiten que la base de datos almacene únicamente información válida.

Imaginemos una tienda que acepta pedidos sin cliente.

Con el tiempo aparecerían registros imposibles de gestionar:

* No sabríamos a quién enviar el pedido.
* No podríamos emitir una factura.
* Tampoco sería posible contactar con el comprador.

El problema no sería técnico.

Sería un error de modelado.

### Las reglas nacen del negocio

Las reglas no las inventa el desarrollador.

Surgen durante las entrevistas con los responsables de la empresa.

Por ejemplo:

> "Cada producto pertenece a una única categoría."

> "Un cliente puede realizar tantos pedidos como desee."

> "Cada pedido debe contener al menos un producto."

Cada una de estas afirmaciones terminará reflejada en el modelo conceptual.

### Tipos de reglas

Aunque existen muchas clasificaciones, en este curso distinguiremos principalmente cuatro tipos.

| Tipo            | Ejemplo                                   |
| ----------------- | ------------------------------------------- |
| Estructurales   | Un pedido pertenece a un cliente.         |
| De cardinalidad | Un cliente puede realizar muchos pedidos. |
| De integridad   | El identificador debe ser único.         |
| Operativas      | Un pedido cancelado no puede modificarse. |

Las reglas estructurales y de cardinalidad aparecerán directamente en el diagrama ER.

Otras se implementarán posteriormente mediante restricciones o lógica de la aplicación.

### Caso práctico

Nuestra empresa comercial ya presenta numerosas reglas de negocio.

Por ejemplo:

* Todo pedido debe pertenecer a un cliente.
* Todo producto pertenece a una categoría.
* Un proveedor puede suministrar varios productos.
* Un cliente puede realizar muchos pedidos.
* Un pedido puede contener varios productos.

Estas reglas determinarán la forma definitiva del modelo conceptual.

### Errores habituales

Un error frecuente consiste en diseñar primero la base de datos y preguntar después cómo funciona la empresa.

El orden correcto es exactamente el contrario.

Primero se comprenden las reglas del negocio y después se diseña el modelo.

### Ideas clave

* Las reglas de negocio describen el funcionamiento real de una organización.
* No dependen del lenguaje SQL ni del SGBD utilizado.
* Se obtienen durante el análisis de requisitos.
* Condicionan el diseño del modelo conceptual.
* Un buen modelo refleja fielmente las reglas del negocio.

