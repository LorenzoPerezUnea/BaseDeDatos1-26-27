# Anomalías de actualización

Una de las consecuencias más peligrosas de la redundancia aparece cuando es necesario modificar información.

Si un mismo dato está almacenado en varios lugares, todos ellos deberán actualizarse.

Cuando alguno se olvida, la base de datos deja de ser consistente.

Esto recibe el nombre de ​**anomalía de actualización**​.

### Un ejemplo

Supongamos la siguiente tabla.

| Pedido | Cliente | Dirección |
| -------: | --------- | ------------ |
|      1 | Ana     | Calle A    |
|      2 | Ana     | Calle A    |
|      3 | Ana     | Calle A    |

Ahora Ana cambia de domicilio.

Su nueva dirección será:

```text
Avenida Central 15
```

Para reflejar este cambio debemos modificar las tres filas.

Si solo actualizamos dos de ellas obtendremos el siguiente resultado.

| Pedido | Cliente | Dirección         |
| -------: | --------- | -------------------- |
|      1 | Ana     | Avenida Central 15 |
|      2 | Ana     | Calle A            |
|      3 | Ana     | Avenida Central 15 |

¿Cuál es ahora la dirección correcta?

La base de datos contiene dos respuestas distintas para la misma pregunta.

### ¿Por qué ocurre?

Porque la dirección pertenece al cliente y no al pedido.

Cada vez que almacenamos un pedido estamos copiando información que realmente ya existe en otro lugar.

### Consecuencias

Las anomalías de actualización provocan:

* información contradictoria;
* pérdida de confianza en los datos;
* errores en informes;
* dificultades para el mantenimiento.

En sistemas empresariales esto puede traducirse en problemas operativos importantes.

### La solución

Separar la información del cliente.

```text
CLIENTE

IdCliente
Nombre
Direccion
```

Y hacer que cada pedido almacene únicamente:

```text
IdCliente
```

Ahora la dirección aparece una única vez.

Cuando cambie, solo será necesario modificar un registro.

### Ideas clave

* Una anomalía de actualización aparece cuando un dato repetido debe modificarse en varios lugares.
* Si alguna copia no se actualiza, la base de datos pierde consistencia.
* La redundancia es la causa principal de este problema.
* La normalización reduce las actualizaciones repetidas.
* Cada dato debería almacenarse una sola vez.

