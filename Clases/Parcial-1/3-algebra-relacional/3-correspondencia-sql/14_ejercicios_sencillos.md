# Ejercicios de Álgebra Relacional: Nivel fácil

## Esquema relacional común

Se utilizará el siguiente esquema de una pequeña tienda:

* ​**CLIENTE**​(`id_cliente`, nombre, ciudad, telefono)
* ​**PRODUCTO**​(`id_producto`, nombre, categoria, precio)
* ​**PEDIDO**​(`id_pedido`, fecha, id\_cliente, estado)

Las claves primarias aparecen indicadas en cada relación. `PEDIDO.id_cliente` es una clave foránea que referencia a `CLIENTE.id_cliente`.

## Ejercicio 1. Selección de productos por precio

### Enunciado

Obtener todos los productos cuyo precio sea superior a 100 euros. El resultado debe incluir todos los atributos de los productos seleccionados.

### Plan de operaciones

1. Seleccionar de la relación `PRODUCTO` las tuplas cuyo precio sea superior a 100.
2. Almacenar el resultado en la relación `PRODUCTOS_CAROS`.

### Notación de álgebra relacional

```
PRODUCTOS_CAROS ← σ precio > 100 (PRODUCTO)
```

## Ejercicio 2. Proyección de nombres y precios

### Enunciado

Obtener una relación que contenga únicamente el nombre y el precio de todos los productos registrados en la tienda. No deben aparecer los demás atributos.

### Plan de operaciones

1. Proyectar los atributos `nombre` y `precio` de la relación `PRODUCTO`.
2. Almacenar el resultado en la relación `NOMBRE_PRECIO_PRODUCTO`.

### Notación de álgebra relacional

```
NOMBRE_PRECIO_PRODUCTO ← π nombre, precio (PRODUCTO)
```

La proyección elimina las columnas no solicitadas y, en el álgebra relacional clásica, también elimina las tuplas duplicadas.

## Ejercicio 3. Clientes de una ciudad

### Enunciado

Obtener todos los datos de los clientes que viven en Santander.

### Plan de operaciones

1. Seleccionar de la relación `CLIENTE` las tuplas cuyo atributo `ciudad` sea igual a `'Santander'`.
2. Almacenar el resultado en la relación `CLIENTES_SANTANDER`.

### Notación de álgebra relacional

```
CLIENTES_SANTANDER ← σ ciudad = 'Santander' (CLIENTE)
```

## Ejercicio 4. Pedidos pendientes

### Enunciado

Obtener todos los datos de los pedidos cuyo estado sea `'Pendiente'`.

### Plan de operaciones

1. Seleccionar de la relación `PEDIDO` las tuplas cuyo estado sea `'Pendiente'`.
2. Almacenar el resultado en la relación `PEDIDOS_PENDIENTES`.

### Notación de álgebra relacional

```
PEDIDOS_PENDIENTES ← σ estado = 'Pendiente' (PEDIDO)
```

## Resumen

En estos cuatro ejercicios se practican las dos operaciones fundamentales del álgebra relacional:

* **Selección (σ):** filtra tuplas según una condición.
* **Proyección (π):** selecciona los atributos que se desean conservar.

Cada expresión genera una nueva relación con nombre propio. Los ejercicios siguientes podrán combinar estas operaciones mediante variables intermedias, manteniendo el mismo estilo de resolución paso a paso.

