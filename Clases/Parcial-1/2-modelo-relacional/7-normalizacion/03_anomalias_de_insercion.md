# Anomalías de inserción

La redundancia no solo ocupa espacio innecesario.

También provoca situaciones en las que la base de datos impide realizar operaciones aparentemente sencillas.

Estas situaciones reciben el nombre de ​**anomalías de inserción**​.

### ¿Qué es una anomalía de inserción?

Una anomalía de inserción ocurre cuando ​**no podemos guardar un dato nuevo sin introducir información que todavía no existe o que no debería ser necesaria**​.

En otras palabras, el diseño de la tabla obliga a almacenar datos irrelevantes o desconocidos para poder realizar una inserción.

### Un ejemplo

Supongamos la siguiente tabla.

| Pedido | Cliente | Dirección | Producto |
| -------: | --------- | ------------ | ---------- |
|      1 | Ana     | Calle A    | Ratón   |
|      2 | Luis    | Calle B    | Monitor  |

Ahora imaginemos que queremos registrar un nuevo cliente llamado Marta.

Todavía no ha realizado ningún pedido.

¿Dónde la almacenamos?

La única tabla disponible exige introducir un número de pedido y un producto.

No podemos guardar únicamente la información del cliente.

### ¿Cuál es el problema?

La tabla está mezclando información de dos entidades distintas:

* clientes;
* pedidos.

La existencia de un cliente no debería depender de que haya realizado un pedido.

Sin embargo, el diseño obliga a ello.

### Otro ejemplo

Supongamos ahora que la empresa incorpora un nuevo producto.

| Producto | Precio |
| ---------- | -------: |
| Webcam   |  59.90 |

Todavía no ha sido vendido.

Si el producto solo puede almacenarse dentro de una tabla de pedidos, tampoco podremos registrarlo.

La base de datos obliga a esperar a que exista una venta.

### La solución

Separar la información.

```text
CLIENTE

IdCliente
Nombre
Direccion
```

```text
PRODUCTO

IdProducto
Nombre
Precio
```

```text
PEDIDO

IdPedido
IdCliente
Fecha
```

```text
LINEAPEDIDO

IdPedido
IdProducto
Cantidad
```

Ahora podemos registrar:

* clientes sin pedidos;
* productos sin ventas;
* pedidos sin necesidad de repetir datos.

### Relación con la normalización

Las anomalías de inserción desaparecen cuando cada entidad posee su propia tabla.

Este será uno de los primeros objetivos de las Formas Normales.

### Ideas clave

* Una anomalía de inserción impide almacenar información válida.
* Suele producirse cuando varias entidades comparten una misma tabla.
* Obliga a introducir datos innecesarios o inexistentes.
* La normalización elimina este problema separando correctamente las entidades.
* Cada tipo de información debe poder almacenarse de forma independiente.

