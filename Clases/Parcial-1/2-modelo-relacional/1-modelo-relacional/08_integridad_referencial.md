# Integridad referencial

Si la integridad de entidad garantiza que cada registro pueda identificarse correctamente, la **integridad referencial** asegura que las relaciones entre tablas permanezcan siempre válidas.

Esta es una de las características que diferencia a las bases de datos relacionales de otros sistemas de almacenamiento de información.

Gracias a ella es posible mantener conexiones coherentes entre clientes, pedidos, productos, facturas y cualquier otro elemento del sistema.

### El problema

Supongamos que existe la siguiente información.

**Clientes**

| IdCliente | Nombre |
| ----------: | -------- |
|         1 | Ana    |
|         2 | Carlos |

**Pedidos**

| IdPedido | IdCliente |
| ---------: | ----------: |
|       10 |         1 |
|       11 |         2 |

Todo parece correcto.

Ahora imaginemos que alguien elimina al cliente número 2.

La tabla **Pedidos** seguiría conteniendo un pedido asociado al cliente 2, pero dicho cliente ya no existiría.

La base de datos contendría una referencia inválida.

### La regla

La integridad referencial establece que:

> **Toda clave foránea debe hacer referencia a una clave primaria existente o contener un valor nulo cuando el diseño lo permita.**

En otras palabras, no podemos crear relaciones con registros inexistentes.

### ¿Cómo actúa un SGBD?

Cuando intentamos insertar o modificar información, el servidor comprueba automáticamente que las referencias sean válidas.

Si intentamos registrar un pedido para un cliente inexistente, MySQL rechazará la operación.

De igual forma, si intentamos eliminar un cliente que todavía posee pedidos asociados, el sistema puede impedir la eliminación o realizar otras acciones previamente configuradas.

### Acciones habituales

Los gestores de bases de datos suelen ofrecer varias posibilidades cuando un registro relacionado se elimina o modifica.

| Acción   | Descripción                                            |
| ----------- | --------------------------------------------------------- |
| RESTRICT  | Impide la operación si existen registros relacionados. |
| CASCADE   | Propaga automáticamente el cambio.                     |
| SET NULL  | Sustituye la referencia por un valor nulo.              |
| NO ACTION | La comprobación se realiza al finalizar la operación. |

Durante las primeras prácticas utilizaremos principalmente **RESTRICT** y, más adelante, estudiaremos el comportamiento de las demás opciones.

### Caso práctico

Nuestra empresa no debería permitir eliminar un cliente que todavía tiene facturas pendientes.

De lo contrario, esas facturas quedarían asociadas a un cliente inexistente.

La integridad referencial evita precisamente este tipo de situaciones.

### Ideas clave

* La integridad referencial mantiene la coherencia entre distintas tablas.
* Las claves foráneas deben apuntar a registros existentes.
* MySQL verifica automáticamente estas relaciones.
* El servidor puede impedir operaciones que rompan la integridad de la base de datos.
* Gracias a esta regla, las relaciones entre entidades permanecen consistentes incluso en bases de datos muy grandes.

