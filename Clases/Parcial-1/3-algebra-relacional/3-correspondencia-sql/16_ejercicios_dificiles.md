# Ejercicios de Álgebra Relacional: Nivel medio (II)

## Esquema relacional común

* ​**CLIENTE**​(`id_cliente`, nombre, ciudad, telefono)
* ​**PRODUCTO**​(`id_producto`, nombre, categoria, precio)
* ​**PEDIDO**​(`id_pedido`, fecha, id\_cliente, estado)

Las claves primarias aparecen indicadas en cada relación. `PEDIDO.id_cliente` es una clave foránea que referencia a `CLIENTE.id_cliente`.

## Ejercicio 9. Unión de clientes de dos ciudades

### Enunciado

Obtener los identificadores de los clientes que viven en Santander o en Bilbao. Cada identificador debe aparecer una sola vez, aunque se cumplan ambas condiciones.

### Plan de operaciones

1. Seleccionar los clientes que viven en Santander.
2. Guardar el resultado en `CLIENTES_SANTANDER`.
3. Proyectar sus identificadores y guardarlos en `ID_SANTANDER`.
4. Seleccionar los clientes que viven en Bilbao.
5. Guardar el resultado en `CLIENTES_BILBAO`.
6. Proyectar sus identificadores y guardarlos en `ID_BILBAO`.
7. Unir ambas relaciones de identificadores.
8. Guardar el resultado en `CLIENTES_SANTANDER_BILBAO`.

### Notación de álgebra relacional

```
CLIENTES_SANTANDER ← σ ciudad = 'Santander' (CLIENTE)

ID_SANTANDER ← π id_cliente (CLIENTES_SANTANDER)

CLIENTES_BILBAO ← σ ciudad = 'Bilbao' (CLIENTE)

ID_BILBAO ← π id_cliente (CLIENTES_BILBAO)

CLIENTES_SANTANDER_BILBAO ← ID_SANTANDER ∪ ID_BILBAO
```

La unión requiere que ambas relaciones tengan el mismo esquema. Si un identificador aparece en ambas, solo figura una vez en el resultado del álgebra relacional clásica.

## Ejercicio 10. Intersección de clientes que cumplen dos condiciones

### Enunciado

Obtener los identificadores de los clientes que viven en Santander y que, además, han realizado al menos un pedido.

### Plan de operaciones

1. Seleccionar los clientes que viven en Santander.
2. Proyectar sus identificadores y guardarlos en `ID_SANTANDER`.
3. Proyectar los identificadores de los clientes que aparecen en `PEDIDO`.
4. Guardar el resultado en `CLIENTES_CON_PEDIDOS`.
5. Calcular la intersección de ambas relaciones.
6. Guardar el resultado en `CLIENTES_SANTANDER_CON_PEDIDOS`.

### Notación de álgebra relacional

```
CLIENTES_SANTANDER ← σ ciudad = 'Santander' (CLIENTE)

ID_SANTANDER ← π id_cliente (CLIENTES_SANTANDER)

CLIENTES_CON_PEDIDOS ← π id_cliente (PEDIDO)

CLIENTES_SANTANDER_CON_PEDIDOS ← ID_SANTANDER ∩ CLIENTES_CON_PEDIDOS
```

La intersección devuelve únicamente los identificadores presentes en ambas relaciones. Como las dos relaciones contienen solo `id_cliente`, sus esquemas son compatibles.

## Ejercicio 11. Diferencia entre clientes con y sin pedidos

### Enunciado

Obtener los identificadores de los clientes que nunca han realizado un pedido.

### Plan de operaciones

1. Proyectar los identificadores de todos los clientes.
2. Guardar el resultado en `TODOS_LOS_CLIENTES`.
3. Proyectar los identificadores que aparecen en los pedidos.
4. Guardar el resultado en `CLIENTES_CON_PEDIDOS`.
5. Restar los clientes con pedidos del conjunto de todos los clientes.
6. Guardar el resultado en `CLIENTES_SIN_PEDIDOS`.

### Notación de álgebra relacional

```
TODOS_LOS_CLIENTES ← π id_cliente (CLIENTE)

CLIENTES_CON_PEDIDOS ← π id_cliente (PEDIDO)

CLIENTES_SIN_PEDIDOS ← TODOS_LOS_CLIENTES − CLIENTES_CON_PEDIDOS
```

La diferencia devuelve las tuplas de la primera relación que no aparecen en la segunda. El orden es importante: invertir los operandos produciría un resultado diferente.

## Ejercicio 12. Clientes y sus pedidos mediante JOIN

### Enunciado

Obtener el nombre de cada cliente junto con el identificador, la fecha y el estado de sus pedidos. Solo deben aparecer los clientes que hayan realizado al menos un pedido.

### Plan de operaciones

1. Combinar `CLIENTE` y `PEDIDO` mediante un JOIN por igualdad de `id_cliente`.
2. Guardar el resultado en `CLIENTES_PEDIDOS`.
3. Proyectar el nombre del cliente, el identificador del pedido, la fecha y el estado.
4. Guardar el resultado en `DETALLE_PEDIDOS_CLIENTES`.

### Notación de álgebra relacional

```
CLIENTES_PEDIDOS ← CLIENTE ⋈ CLIENTE.id_cliente = PEDIDO.id_cliente PEDIDO

DETALLE_PEDIDOS_CLIENTES ← π CLIENTE.nombre, PEDIDO.id_pedido, PEDIDO.fecha, PEDIDO.estado (CLIENTES_PEDIDOS)
```

El JOIN combina cada cliente con los pedidos cuyo `id_cliente` coincide con el suyo. Los clientes que no tienen pedidos no aparecen porque se utiliza un JOIN interno.

## Resumen

Estos cuatro ejercicios amplían las operaciones disponibles:

* **Unión (∪):** reúne las tuplas de dos relaciones compatibles y elimina duplicados.
* **Intersección (∩):** conserva las tuplas que aparecen en ambas relaciones.
* **Diferencia (−):** conserva las tuplas de la primera relación que no aparecen en la segunda.
* **JOIN (⋈):** combina tuplas de relaciones diferentes que satisfacen una condición de unión.

Las operaciones de unión, intersección y diferencia requieren relaciones con esquemas compatibles. El JOIN permite combinar relaciones con atributos distintos mediante una condición de correspondencia.

En todos los ejercicios, las relaciones intermedias se asignan a variables y se reutilizan en pasos posteriores, sin expresiones anidadas.

## Ejercicio 13. Cadena de JOIN: clientes, pedidos y productos

### Enunciado

Obtener el nombre de cada cliente, el identificador y la fecha de sus pedidos, y el nombre y el precio de los productos incluidos en dichos pedidos.

Para resolver el ejercicio, se dispone de las siguientes relaciones:

* ​**CLIENTE**​(`id_cliente`, nombre, ciudad, telefono)
* ​**PEDIDO**​(`id_pedido`, fecha, id\_cliente, estado)
* ​**DETALLE\_PEDIDO**​(`id_pedido`, `id_producto`, cantidad, precio\_unitario)
* ​**PRODUCTO**​(`id_producto`, nombre, categoria, precio)

Las claves primarias de `DETALLE_PEDIDO` son la combinación de `id_pedido` e `id_producto`. Ambos atributos son claves foráneas que referencian a `PEDIDO` y `PRODUCTO`, respectivamente.

Se deben mostrar únicamente los clientes que hayan realizado pedidos que contengan productos.

### Plan de operaciones

1. Combinar `CLIENTE` y `PEDIDO` mediante el atributo `id_cliente`.
2. Almacenar el resultado en `CLIENTES_PEDIDOS`.
3. Combinar `CLIENTES_PEDIDOS` con `DETALLE_PEDIDO` mediante `id_pedido`.
4. Almacenar el resultado en `PEDIDOS_CON_DETALLE`.
5. Combinar `PEDIDOS_CON_DETALLE` con `PRODUCTO` mediante `id_producto`.
6. Almacenar el resultado en `PEDIDOS_PRODUCTOS`.
7. Proyectar el nombre del cliente, el identificador y la fecha del pedido, el nombre del producto, la cantidad y el precio unitario.
8. Almacenar el resultado final en `RESULTADO_EJ13`.

### Notación de álgebra relacional

```
CLIENTE_REN ← ρ nombre_cliente ← nombre (CLIENTE)

PRODUCTO_REN ← ρ nombre_producto ← nombre (PRODUCTO)

CLIENTES_PEDIDOS ← CLIENTE_REN ⋈ CLIENTE_REN.id_cliente = PEDIDO.id_cliente PEDIDO

PEDIDOS_CON_DETALLE ← CLIENTES_PEDIDOS ⋈ CLIENTES_PEDIDOS.id_pedido = DETALLE_PEDIDO.id_pedido DETALLE_PEDIDO

PEDIDOS_PRODUCTOS ← PEDIDOS_CON_DETALLE ⋈ DETALLE_PEDIDO.id_producto = PRODUCTO_REN.id_producto PRODUCTO_REN

RESULTADO_EJ13 ← π nombre_cliente, id_pedido, fecha, nombre_producto, cantidad, precio_unitario (PEDIDOS_PRODUCTOS)
```

### Observaciones

* Cada JOIN utiliza la relación obtenida en el paso anterior, formando una cadena de tres JOIN.
* Se emplean JOIN internos, por lo que solo aparecen clientes con pedidos que contienen detalles asociados a productos existentes.
* Se conserva `precio_unitario` de `DETALLE_PEDIDO`, porque representa el precio aplicado en el pedido. El atributo `PRODUCTO.precio` podría haber cambiado posteriormente.
* En una implementación con relaciones intermedias, es conveniente calificar los atributos con el nombre de su relación original para evitar ambigüedades.

