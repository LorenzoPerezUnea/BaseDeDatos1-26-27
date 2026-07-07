# Reglas de integridad

Una base de datos no solo debe almacenar información.

También debe garantizar que esa información sea ​**correcta, coherente y consistente**​.

Las normas encargadas de mantener esa calidad reciben el nombre de ​**reglas de integridad**​.

Aunque estudiaremos su implementación en MySQL más adelante, es importante comprenderlas desde el modelo conceptual.

### ¿Qué significa integridad?

La palabra *integridad* hace referencia a que los datos representan fielmente la realidad del negocio.

Una base de datos íntegra evita situaciones imposibles como:

* Pedidos sin cliente.
* Productos con precios negativos.
* Dos clientes con el mismo identificador.
* Facturas asociadas a pedidos inexistentes.

El objetivo es impedir que se almacene información inválida.

### Integridad de entidad

La primera gran regla establece que cada entidad debe poder identificarse de forma única.

Por ello todas las entidades poseen un identificador.

Por ejemplo:

```text
Cliente

IdCliente
Nombre
Email
```

Dos clientes diferentes nunca deberían compartir el mismo identificador.

Esta regla garantiza que podamos localizar cualquier instancia sin ambigüedad.

### Integridad referencial

La segunda gran regla afecta a las relaciones entre entidades.

Supongamos que un pedido pertenece al cliente número 25.

Si ese cliente no existe, la relación deja de tener sentido.

Por tanto:

Toda relación debe apuntar a una entidad válida.

Este principio será fundamental cuando aparezcan las claves foráneas en el modelo relacional.

### Integridad del dominio

Cada atributo admite únicamente determinados valores.

Por ejemplo:

| Atributo    | Valores válidos           |
| ------------- | ---------------------------- |
| Precio      | Mayor que 0                |
| Stock       | Entero igual o mayor que 0 |
| Email       | Formato válido            |
| FechaPedido | Fecha existente            |

Estas restricciones evitan datos absurdos o imposibles.

### Integridad definida por el negocio

Cada empresa añade además sus propias reglas.

Por ejemplo:

* Un pedido debe contener al menos un producto.
* Una factura solo puede emitirse para un pedido confirmado.
* No puede venderse un producto descatalogado.

Estas normas no son universales.

Dependen exclusivamente del funcionamiento de cada organización.

### Caso práctico

Nuestro sistema incorporará progresivamente reglas como:

* Todo cliente posee un identificador único.
* Todo pedido pertenece a un cliente existente.
* Todo producto pertenece a una categoría válida.
* El precio de un producto debe ser positivo.
* El stock nunca puede ser negativo.

Estas reglas terminarán implementándose mediante restricciones SQL.

### Ideas clave

* La integridad garantiza la calidad de la información almacenada.
* Existen reglas de integridad de entidad, referencial y de dominio.
* Cada empresa incorpora además restricciones propias.
* Las reglas de integridad nacen durante el análisis del negocio.
* Más adelante se implementarán mediante restricciones del SGBD.

