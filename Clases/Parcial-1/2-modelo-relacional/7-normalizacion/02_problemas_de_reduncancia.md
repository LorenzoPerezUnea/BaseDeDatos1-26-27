# Problemas de redundancia

La palabra **redundancia** significa que una misma información aparece almacenada varias veces dentro de la base de datos.

Aunque en algunos casos esto pueda parecer inofensivo, constituye el origen de la mayoría de los problemas que intenta resolver la normalización.

### ¿Qué entendemos por información repetida?

Consideremos la siguiente tabla.

| Pedido | Cliente | Dirección | Producto |
| -------: | --------- | ------------ | ---------- |
|      1 | Ana     | Calle A    | Ratón   |
|      1 | Ana     | Calle A    | Teclado  |
|      2 | Ana     | Calle A    | Monitor  |

Observemos que el nombre del cliente y su dirección aparecen repetidos tres veces.

Sin embargo, Ana solo tiene una dirección.

Estamos almacenando el mismo dato una y otra vez.

### ¿Por qué ocurre?

La causa suele ser que mezclamos en una misma tabla información perteneciente a entidades diferentes.

En este ejemplo aparecen simultáneamente datos de:

* pedidos;
* clientes;
* productos.

Cada vez que añadimos un producto al pedido también repetimos la información del cliente.

### Consecuencias

La redundancia produce numerosos inconvenientes.

* Aumenta el tamaño de la base de datos.
* Incrementa el tiempo de actualización.
* Favorece la aparición de inconsistencias.
* Hace más complejas las modificaciones futuras.

En sistemas pequeños estos problemas pueden pasar desapercibidos.

En sistemas con millones de registros pueden convertirse en un serio obstáculo.

### Un ejemplo práctico

Supongamos que Ana cambia de domicilio.

Si la dirección aparece en cincuenta pedidos distintos, habrá que modificar cincuenta registros.

Basta olvidar uno para que la información deje de ser coherente.

La base de datos ya no sabrá cuál es la dirección correcta.

### La solución

En lugar de repetir la dirección en todos los pedidos, basta con almacenarla una única vez en la tabla CLIENTE.

Los pedidos únicamente necesitarán guardar el identificador del cliente.

Este principio será el eje de todas las Formas Normales.

### Ideas clave

* La redundancia consiste en almacenar el mismo dato varias veces.
* Suele aparecer cuando mezclamos distintas entidades en una misma tabla.
* Produce inconsistencias y aumenta el coste de mantenimiento.
* La normalización busca eliminar la redundancia innecesaria.
* Cada dato debería almacenarse únicamente donde realmente pertenece.

