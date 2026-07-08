# Segunda Forma Normal

Una vez alcanzada la Primera Forma Normal, todavía pueden existir redundancias importantes.

La **Segunda Forma Normal (2FN)** aparece para resolver un problema muy concreto:

> **Las dependencias parciales.**

Recordemos que una dependencia parcial ocurre cuando un atributo depende únicamente de una parte de una clave primaria compuesta.

### Requisitos

Una relación se encuentra en Segunda Forma Normal cuando:

1. Ya está en Primera Forma Normal.
2. No existen dependencias parciales.

Es decir, todos los atributos no clave deben depender de la ​**clave completa**​.

### Un ejemplo

Supongamos la siguiente tabla.

| IdPedido | IdProducto | NombreProducto | Cantidad |
| ---------: | -----------: | ---------------- | ---------: |
|        1 |        101 | Ratón         |        2 |
|        1 |        102 | Teclado        |        1 |
|        2 |        101 | Ratón         |        3 |

La clave primaria es:

```text
(IdPedido, IdProducto)
```

Analicemos las dependencias.

```text
(IdPedido, IdProducto)
→ Cantidad
```

Hasta aquí todo es correcto.

Sin embargo:

```text
IdProducto
→ NombreProducto
```

Aquí aparece una dependencia parcial.

El nombre del producto no depende del pedido.

Solo depende del producto.

### El problema

Cada vez que un producto aparece en un pedido repetimos su nombre.

Esto produce redundancia y anomalías de actualización.

### La solución

Dividir la tabla.

```text
PRODUCTO

IdProducto
NombreProducto
```

```text
LINEAPEDIDO

IdPedido
IdProducto
Cantidad
```

Ahora cada dato se almacena exactamente donde corresponde.

La redundancia desaparece.

### ¿Cuándo puede incumplirse?

Solo cuando existe una ​**clave primaria compuesta**​.

Si la clave primaria contiene un único atributo, la Segunda Forma Normal se cumple automáticamente.

### Preparación para la siguiente sección

Eliminar las dependencias parciales mejora notablemente el diseño.

Sin embargo, todavía pueden quedar dependencias entre atributos no clave.

Ese será precisamente el problema que resolverá la ​**Tercera Forma Normal**​.

### Ideas clave

* La Segunda Forma Normal elimina dependencias parciales.
* Solo afecta a tablas con claves primarias compuestas.
* Todos los atributos deben depender de la clave completa.
* La solución consiste en separar la información en nuevas tablas.
* La Segunda Forma Normal reduce considerablemente la redundancia.

