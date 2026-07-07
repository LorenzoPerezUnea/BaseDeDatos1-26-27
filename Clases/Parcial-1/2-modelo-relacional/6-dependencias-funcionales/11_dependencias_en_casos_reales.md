# Dependencias en casos reales

Hasta ahora hemos trabajado con ejemplos muy pequeños para facilitar la comprensión de los conceptos.

Sin embargo, las dependencias funcionales adquieren su verdadera utilidad cuando se aplican a bases de datos reales.

Analicemos algunas situaciones de nuestro caso de estudio.

### Caso 1. Clientes

Tabla CLIENTE.

| Atributo  |
| ----------- |
| IdCliente |
| Nombre    |
| Apellidos |
| Correo    |
| Teléfono |

Las principales dependencias son:

```text
IdCliente → Nombre

IdCliente → Apellidos

IdCliente → Correo

IdCliente → Telefono
```

Todas ellas proceden del hecho de que el identificador distingue unívocamente a cada cliente.

### Caso 2. Productos

Tabla PRODUCTO.

| Atributo    |
| ------------- |
| IdProducto  |
| Nombre      |
| Precio      |
| Stock       |
| IdCategoria |

Dependencias.

```text
IdProducto → Nombre

IdProducto → Precio

IdProducto → Stock

IdProducto → IdCategoria
```

Si además almacenáramos el nombre de la categoría aparecería una dependencia transitiva.

```text
IdCategoria → NombreCategoria
```

Este detalle será muy importante durante la normalización.

### Caso 3. Pedidos

Tabla PEDIDO.

```text
IdPedido → Fecha

IdPedido → Estado

IdPedido → IdCliente

IdPedido → IdEmpleado
```

Cada pedido determina completamente su información.

### Caso 4. Línea de pedido

```text
(IdPedido, IdProducto)
→
Cantidad
```

Aquí observamos una dependencia completa.

Los dos atributos son necesarios para determinar la cantidad.

### Aprender a descubrir dependencias

Una buena práctica consiste en hacerse siempre la misma pregunta.

> Si conozco este atributo, ¿puedo conocer necesariamente el otro?

Si la respuesta es sí debido a una regla del negocio, probablemente exista una dependencia funcional.

### Ideas clave

* Las dependencias funcionales aparecen en cualquier sistema de información.
* Proceden de las reglas del negocio.
* Analizarlas correctamente permite construir modelos más robustos.
* El caso de estudio servirá como referencia durante toda la normalización.
* Saber descubrir dependencias es una habilidad fundamental para cualquier diseñador de bases de datos.

