# Integridad referencial

Una base de datos relacional no solo almacena información.

También debe garantizar que las relaciones entre las tablas permanezcan siempre correctas.

Este objetivo se consigue mediante la ​**integridad referencial**​.

### ¿Qué significa?

La integridad referencial asegura que una clave foránea siempre haga referencia a un registro existente.

Por ejemplo, si un pedido pertenece a un cliente, dicho cliente debe existir realmente en la tabla CLIENTE.

No tendría sentido almacenar:

```text
PEDIDO

IdCliente = 999
```

si el cliente 999 no existe.

### Un ejemplo

Supongamos las siguientes tablas.

```text
CLIENTE

IdCliente
Nombre
```

```text
PEDIDO

IdPedido

IdCliente
```

Si intentamos registrar un pedido para un cliente inexistente, el sistema deberá impedirlo.

De esta manera evitamos referencias inválidas y datos inconsistentes.

### ¿Qué ocurre al eliminar un registro?

Imaginemos ahora que queremos borrar un cliente que ya tiene pedidos registrados.

¿Qué debería hacer la base de datos?

Existen varias posibilidades.

* Impedir el borrado.
* Eliminar también los pedidos relacionados.
* Mantener los pedidos asignándoles otro valor permitido.
* Permitir el borrado únicamente cuando no existan referencias.

La decisión dependerá de las reglas del negocio.

Por ello, la integridad referencial no solo protege los datos, sino que también refleja el funcionamiento real de la organización.

### Integridad y reglas de negocio

En nuestra empresa comercial no tendría sentido eliminar un cliente y perder automáticamente todo su historial de pedidos.

Por ello, lo más razonable será impedir el borrado mientras existan pedidos asociados.

Más adelante veremos cómo definir este comportamiento mediante restricciones SQL.

### Ideas clave

* La integridad referencial mantiene la coherencia entre tablas.
* Toda clave foránea debe apuntar a un registro existente.
* El sistema debe controlar qué ocurre al modificar o eliminar registros relacionados.
* Las decisiones dependen de las reglas del negocio.
* La integridad referencial constituye uno de los pilares del Modelo Relacional.

