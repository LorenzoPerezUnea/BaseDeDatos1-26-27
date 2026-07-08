# Anomalías de borrado

El tercer gran problema provocado por la redundancia aparece cuando eliminamos información.

En ocasiones, al borrar un registro también desaparecen otros datos que todavía eran importantes.

Este fenómeno recibe el nombre de ​**anomalía de borrado**​.

### ¿Qué ocurre?

Imaginemos la siguiente tabla.

| Pedido | Cliente | Producto |
| -------: | --------- | ---------- |
|      1 | Ana     | Ratón   |
|      2 | Luis    | Monitor  |

Supongamos que Ana únicamente ha realizado un pedido.

Si ese pedido se elimina porque fue cancelado, también desaparecerá toda la información del cliente.

Aunque Ana siga siendo cliente de la empresa, ya no existirá ningún registro sobre ella.

### Otro ejemplo

Supongamos ahora una tabla que almacena productos vendidos.

| Pedido | Producto |
| -------: | ---------- |
|      8 | Webcam   |

Si eliminamos ese único pedido también desaparecerá cualquier referencia al producto Webcam.

La empresa olvidará incluso que dicho producto existe.

### ¿Por qué sucede?

Porque estamos mezclando en una única tabla información que pertenece a entidades diferentes.

El pedido es un hecho temporal.

El cliente y el producto representan información permanente.

Eliminar un pedido no debería implicar borrar clientes o productos.

### La solución

Separar cada entidad en su propia tabla.

```text
CLIENTE
```

```text
PRODUCTO
```

```text
PEDIDO
```

```text
LINEAPEDIDO
```

Ahora podemos eliminar un pedido sin perder la información de clientes o productos.

Solo desaparecerá aquello que realmente queremos eliminar.

### Comparación de anomalías

| Tipo           | Problema                                           |
| ---------------- | ---------------------------------------------------- |
| Inserción     | No podemos guardar información nueva.             |
| Actualización | Debemos modificar el mismo dato en varios lugares. |
| Borrado        | Eliminamos información que no queríamos perder.  |

Estas tres anomalías constituyen la principal motivación para aplicar la normalización.

### Ideas clave

* Una anomalía de borrado elimina información válida de forma accidental.
* Se produce cuando varias entidades comparten una misma tabla.
* Los datos permanentes no deben depender de datos temporales.
* La normalización separa las entidades para evitar pérdidas de información.
* Eliminar un registro no debería afectar a información independiente.

