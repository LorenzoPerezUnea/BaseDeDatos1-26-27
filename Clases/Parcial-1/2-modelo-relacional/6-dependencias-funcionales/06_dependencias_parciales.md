# Dependencias parciales

En la sección anterior vimos que una dependencia es **completa** cuando todos los atributos de una clave compuesta son necesarios para determinar otro atributo.

Pero ¿qué ocurre si únicamente se necesita una parte de esa clave?

En ese caso hablamos de una ​**dependencia funcional parcial**​.

Las dependencias parciales son especialmente importantes porque constituyen el principal problema que intenta eliminar la ​**Segunda Forma Normal (2FN)**​.

### Un ejemplo

Consideremos la siguiente tabla.

| IdPedido | IdProducto | NombreProducto | Cantidad |
| ---------: | -----------: | ---------------- | ---------: |
|       15 |        101 | Ratón         |        2 |
|       15 |        104 | Monitor        |        1 |
|       16 |        101 | Ratón         |        5 |

Supongamos que la clave primaria es:

```text
(IdPedido, IdProducto)
```

Ahora analicemos la siguiente dependencia.

```text
IdProducto → NombreProducto
```

### ¿Por qué es parcial?

Porque **NombreProducto** depende únicamente de ​**IdProducto**​.

No necesita conocer ​**IdPedido**​.

Sin embargo, la clave primaria está formada por ambos atributos.

Por tanto, el atributo **NombreProducto** depende solamente de una parte de la clave.

Eso constituye una dependencia parcial.

### El problema

Este diseño provoca redundancia.

| IdPedido | IdProducto | NombreProducto |
| ---------: | -----------: | ---------------- |
|       15 |        101 | Ratón         |
|       16 |        101 | Ratón         |
|       18 |        101 | Ratón         |

El nombre del producto aparece repetido una y otra vez.

Si mañana cambiamos "Ratón" por "Ratón inalámbrico", habrá que modificar todas las filas.

Esto aumenta el riesgo de inconsistencias.

### La solución

La información del producto debe almacenarse únicamente en la tabla PRODUCTO.

```text
PRODUCTO

----------------------
IdProducto
NombreProducto
Precio
Stock
```

Mientras tanto, LINEAPEDIDO conservará únicamente la referencia al producto.

```text
LINEAPEDIDO

----------------------
IdPedido
IdProducto
Cantidad
```

Ahora el nombre solo existe en un único lugar.

### ¿Cuándo aparecen?

Las dependencias parciales únicamente pueden aparecer cuando existe una ​**clave compuesta**​.

Si una tabla posee una clave primaria formada por un solo atributo, no puede haber dependencias parciales.

### Ideas clave

* Una dependencia parcial utiliza únicamente parte de una clave compuesta.
* Genera redundancia de información.
* Es una de las principales causas de anomalías de actualización.
* La Segunda Forma Normal elimina este tipo de dependencias.
* Detectarlas mejora significativamente el diseño de la base de datos.

