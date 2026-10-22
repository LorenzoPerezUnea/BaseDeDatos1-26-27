# Ejercicios de Álgebra Relacional: Nivel medio

## Esquema relacional común

Se utilizará el siguiente esquema de una pequeña tienda:

* ​**CLIENTE**​(`id_cliente`, nombre, ciudad, telefono)
* ​**PRODUCTO**​(`id_producto`, nombre, categoria, precio)
* ​**PEDIDO**​(`id_pedido`, fecha, id\_cliente, estado)

Las claves primarias aparecen indicadas en cada relación. `PEDIDO.id_cliente` es una clave foránea que referencia a `CLIENTE.id_cliente`.

## Ejercicio 5. Productos de una categoría con precio limitado

### Enunciado

Obtener los nombres y precios de los productos de la categoría `'Informática'` cuyo precio sea inferior a 500 euros.

### Plan de operaciones

1. Seleccionar los productos cuya categoría sea `'Informática'`.
2. Almacenar el resultado en `PRODUCTOS_INFORMATICA`.
3. Seleccionar, de esa relación, los productos cuyo precio sea inferior a 500.
4. Almacenar el resultado en `INFORMATICA_BARATA`.
5. Proyectar el nombre y el precio de los productos seleccionados.
6. Almacenar el resultado en `RESULTADO_EJ5`.

### Notación de álgebra relacional

```
PRODUCTOS_INFORMATICA ← σ categoria = 'Informática' (PRODUCTO)

INFORMATICA_BARATA ← σ precio < 500 (PRODUCTOS_INFORMATICA)

RESULTADO_EJ5 ← π nombre, precio (INFORMATICA_BARATA)
```

## Ejercicio 6. Clientes que han realizado pedidos

### Enunciado

Obtener los identificadores de los clientes que han realizado al menos un pedido. El resultado no debe contener identificadores repetidos.

### Plan de operaciones

1. Proyectar el atributo `id_cliente` de la relación `PEDIDO`.
2. Almacenar el resultado en `CLIENTES_CON_PEDIDOS`.

### Notación de álgebra relacional

```
CLIENTES_CON_PEDIDOS ← π id_cliente (PEDIDO)
```

La proyección elimina los identificadores repetidos en el álgebra relacional clásica. No es necesario combinar la relación `PEDIDO` con `CLIENTE`, porque solo se solicitan los identificadores presentes en los pedidos.

## Ejercicio 7. Clientes que no han realizado pedidos

### Enunciado

Obtener los identificadores de los clientes que todavía no han realizado ningún pedido.

### Plan de operaciones

1. Obtener los identificadores de todos los clientes.
2. Almacenar el resultado en `TODOS_LOS_CLIENTES`.
3. Obtener los identificadores de los clientes que aparecen en algún pedido.
4. Almacenar el resultado en `CLIENTES_CON_PEDIDOS`.
5. Restar del conjunto de todos los clientes aquellos que han realizado pedidos.
6. Almacenar el resultado en `CLIENTES_SIN_PEDIDOS`.

### Notación de álgebra relacional

```
TODOS_LOS_CLIENTES ← π id_cliente (CLIENTE)

CLIENTES_CON_PEDIDOS ← π id_cliente (PEDIDO)

CLIENTES_SIN_PEDIDOS ← TODOS_LOS_CLIENTES − CLIENTES_CON_PEDIDOS
```

Ambas relaciones que intervienen en la diferencia tienen el mismo esquema: un único atributo, `id_cliente`. Por tanto, la operación está correctamente definida.

## Ejercicio 8. Pares de productos con el mismo precio

### Enunciado

Obtener los pares de productos distintos que tienen exactamente el mismo precio. Cada resultado debe mostrar el identificador y el nombre de ambos productos. No deben aparecer pares en los que un producto se compare consigo mismo ni pares duplicados en orden inverso.

### Plan de operaciones

1. Renombrar la relación `PRODUCTO` para representar los productos como candidatos al primer elemento del par.
2. Almacenar el resultado en `PRODUCTO_A`.
3. Renombrar de nuevo `PRODUCTO` para representar los candidatos al segundo elemento del par.
4. Almacenar el resultado en `PRODUCTO_B`.
5. Calcular el producto cartesiano entre ambas relaciones.
6. Almacenar el resultado en `PARES_CANDIDATOS`.
7. Seleccionar los pares que tienen el mismo precio y cuyo identificador del primer producto es menor que el del segundo.
8. Almacenar el resultado en `PARES_MISMO_PRECIO`.
9. Proyectar los identificadores y nombres de ambos productos.
10. Almacenar el resultado en `RESULTADO_EJ8`.

### Notación de álgebra relacional

```
PRODUCTO_A ← ρ id_producto_A ← id_producto, nombre_A ← nombre, precio_A ← precio (PRODUCTO)

PRODUCTO_B ← ρ id_producto_B ← id_producto, nombre_B ← nombre, precio_B ← precio (PRODUCTO)

PARES_CANDIDATOS ← PRODUCTO_A × PRODUCTO_B

PARES_MISMO_PRECIO ← σ precio_A = precio_B AND id_producto_A < id_producto_B (PARES_CANDIDATOS)

RESULTADO_EJ8 ← π id_producto_A, nombre_A, id_producto_B, nombre_B (PARES_MISMO_PRECIO)
```

El renombrado permite distinguir los atributos de cada copia de `PRODUCTO`. La condición `A.id_producto < B.id_producto` evita comparar un producto consigo mismo y elimina la duplicación por orden inverso: si se obtiene el par A–B, no se obtiene también B–A.

## Resumen

En estos ejercicios se practican:

* Composición secuencial de selección y proyección.
* Obtención de identificadores mediante proyección sin duplicados.
* Diferencia entre relaciones compatibles.
* Renombrado y producto cartesiano.
* Selección sobre pares de tuplas mediante condiciones que comparan atributos de dos relaciones.

En todos los casos, cada operación genera una relación intermedia identificada por una variable. No se anidan expresiones.

