# Soluciones guiadas — Bloque 2. Producto cartesiano y JOIN

## Introducción

En este segundo bloque aparecen las primeras consultas que requieren combinar información almacenada en varias relaciones.

Hasta ahora todas las consultas podían resolverse trabajando sobre una única relación. Sin embargo, en una base de datos relacional la información suele distribuirse entre múltiples tablas para evitar redundancias y mantener la integridad de los datos.

Por ello es necesario aprender a reconstruir esa información mediante operaciones de combinación.

Aunque el **JOIN (⋈)** puede definirse formalmente como un **producto cartesiano (×)** seguido de una ​**selección (σ)**​, en la práctica utilizaremos el operador JOIN por ser más claro y más cercano a la forma en que posteriormente escribiremos consultas SQL.

Al igual que en el bloque anterior, el solucionario utilizará como formato recomendado la resolución mediante ​**relaciones intermedias**​.

Esta forma de escribir las consultas facilita tanto la corrección como la comprensión del proceso de construcción de una consulta compleja.

Durante todos los ejercicios utilizaremos el siguiente modelo simplificado de la empresa:

* Cliente(IdCliente, Nombre, Ciudad)
* Pedido(IdPedido, IdCliente, Fecha)
* LineaPedido(IdPedido, IdProducto, Cantidad)
* Producto(IdProducto, Nombre, Categoria, Precio)

---

# Ejercicio 1

### Enunciado

La dirección comercial desea conocer el nombre de todos los clientes que han realizado algún pedido.

### Solución

```text
R1 ← Cliente ⋈ Cliente.IdCliente = Pedido.IdCliente Pedido

R2 ← π Cliente.Nombre (R1)

Resultado ← R2
```

### Explicación

El JOIN relaciona cada cliente con los pedidos que ha realizado.

Posteriormente se proyecta únicamente el atributo solicitado.

---

# Ejercicio 2

### Enunciado

Obtener el identificador de todos los pedidos realizados por clientes de Santander.

### Solución

```text
R1 ← σ Ciudad='Santander' (Cliente)

R2 ← R1 ⋈ R1.IdCliente = Pedido.IdCliente Pedido

R3 ← π IdPedido (R2)

Resultado ← R3
```

### Explicación

Se comienza reduciendo el número de clientes mediante una selección.

Después se realiza el JOIN únicamente con esos clientes.

---

# Ejercicio 3

### Enunciado

Mostrar el nombre de los productos incluidos en el pedido 1003.

### Solución

```text
R1 ← σ IdPedido=1003 (Pedido)

R2 ← R1 ⋈ R1.IdPedido = LineaPedido.IdPedido LineaPedido

R3 ← R2 ⋈ LineaPedido.IdProducto = Producto.IdProducto Producto

R4 ← π Producto.Nombre (R3)

Resultado ← R4
```

### Explicación

La consulta sigue el recorrido natural:

Pedido

→ LíneaPedido

→ Producto

Filtrar el pedido al principio reduce considerablemente el trabajo posterior.

---

# Ejercicio 4

### Enunciado

Obtener el nombre de los clientes que han comprado un producto de la categoría ​**Periféricos**​.

### Solución

```text
R1 ← σ Categoria='Periféricos' (Producto)

R2 ← R1 ⋈ R1.IdProducto = LineaPedido.IdProducto LineaPedido

R3 ← R2 ⋈ LineaPedido.IdPedido = Pedido.IdPedido Pedido

R4 ← R3 ⋈ Pedido.IdCliente = Cliente.IdCliente Cliente

R5 ← π Cliente.Nombre (R4)

Resultado ← R5
```

### Explicación

En lugar de comenzar desde Cliente, resulta más eficiente comenzar desde Producto, ya que la selección sobre la categoría reduce el número de registros desde el primer paso.

---

# Ejercicio 5

### Enunciado

Mostrar el nombre y la cantidad de todos los productos vendidos en el pedido 1001.

### Solución

```text
R1 ← σ IdPedido=1001 (Pedido)

R2 ← R1 ⋈ R1.IdPedido = LineaPedido.IdPedido LineaPedido

R3 ← R2 ⋈ LineaPedido.IdProducto = Producto.IdProducto Producto

R4 ← π Producto.Nombre, Cantidad (R3)

Resultado ← R4
```

### Explicación

La cantidad pertenece a LineaPedido mientras que el nombre pertenece a Producto.

Es necesario combinar ambas relaciones antes de realizar la proyección.

---

# Ejercicio 6

### Enunciado

La empresa desea conocer todos los pedidos realizados por clientes de Bilbao.

### Solución

```text
R1 ← σ Ciudad='Bilbao' (Cliente)

R2 ← R1 ⋈ R1.IdCliente = Pedido.IdCliente Pedido

R3 ← π IdPedido (R2)

Resultado ← R3
```

### Explicación

El procedimiento es idéntico al ejercicio anterior, modificando únicamente la condición de selección.

---

# Ejercicio 7

### Enunciado

¿Qué ocurriría si realizáramos un producto cartesiano entre Cliente y Producto sin aplicar posteriormente ninguna condición de selección?

### Solución

```text
R1 ← Cliente × Producto

Resultado ← R1
```

### Explicación

El producto cartesiano genera **todas las combinaciones posibles** entre ambas relaciones.

Si existen:

* 6 clientes
* 6 productos

el resultado contendrá:

```text
|Cliente × Producto|

=

6 × 6

=

36 tuplas
```

La inmensa mayoría de esas combinaciones carecen de significado.

Precisamente por ello el producto cartesiano rara vez se utiliza de forma aislada.

---

# Ejercicio 8

### Enunciado

Calcular cuántas tuplas produciría el producto cartesiano entre Cliente y Producto.

### Solución

```text
|Cliente × Producto|

=

|Cliente| × |Producto|

=

6 × 6

=

36 tuplas
```

### Explicación

No es necesario construir el producto cartesiano.

Basta multiplicar las cardinalidades de ambas relaciones.

---

# Ejercicio 9

### Enunciado

Obtener el nombre de los clientes que compraron el producto ​**SSD 1 TB**​.

### Solución

```text
R1 ← σ Nombre='SSD 1 TB' (Producto)

R2 ← R1 ⋈ R1.IdProducto = LineaPedido.IdProducto LineaPedido

R3 ← R2 ⋈ LineaPedido.IdPedido = Pedido.IdPedido Pedido

R4 ← R3 ⋈ Pedido.IdCliente = Cliente.IdCliente Cliente

R5 ← π Cliente.Nombre (R4)

Resultado ← R5
```

### Explicación

Comenzar por el producto permite reducir inmediatamente el conjunto de datos antes de recorrer el resto de relaciones.

---

# Ejercicio 10

### Enunciado

La empresa desea elaborar un listado que muestre:

* nombre del cliente;
* nombre del producto;
* cantidad comprada.

### Solución

```text
R1 ← Cliente ⋈ Cliente.IdCliente = Pedido.IdCliente Pedido

R2 ← R1 ⋈ Pedido.IdPedido = LineaPedido.IdPedido LineaPedido

R3 ← R2 ⋈ LineaPedido.IdProducto = Producto.IdProducto Producto

R4 ← π Cliente.Nombre,
         Producto.Nombre,
         Cantidad
     (R3)

Resultado ← R4
```

### Explicación

La consulta requiere combinar las cuatro relaciones principales del modelo antes de proyectar los atributos solicitados.

---

# Ejercicio 11

### Enunciado

Explica con tus propias palabras por qué el JOIN puede entenderse como un producto cartesiano seguido de una selección.

### Solución

La equivalencia formal es:

```text
R ⋈R.A=S.B S

≡

σR.A=S.B(R × S)
```

Es decir:

```text
R1 ← R × S

R2 ← σ R.A=S.B (R1)

Resultado ← R2
```

### Explicación

El producto cartesiano genera todas las combinaciones posibles.

La selección elimina posteriormente aquellas combinaciones que no cumplen la condición de unión.

El operador JOIN no es más que una notación abreviada para expresar ambas operaciones de forma más clara.

---

# Ejercicio 12

### Enunciado

Observa la siguiente secuencia de operadores.

Cliente

↓

JOIN Pedido

↓

JOIN LineaPedido

↓

JOIN Producto

↓

Proyección (NombreCliente, NombreProducto)

### Solución

```text
R1 ← Cliente ⋈ Cliente.IdCliente = Pedido.IdCliente Pedido

R2 ← R1 ⋈ Pedido.IdPedido = LineaPedido.IdPedido LineaPedido

R3 ← R2 ⋈ LineaPedido.IdProducto = Producto.IdProducto Producto

R4 ← π Cliente.Nombre,
         Producto.Nombre
     (R3)

Resultado ← R4
```

### Explicación

La consulta devuelve el nombre de cada cliente junto con los productos incluidos en sus pedidos.

No es necesaria ninguna selección porque el enunciado no establece restricciones adicionales.

---

# Observaciones para la corrección

Los errores más frecuentes en este bloque son:

* intentar unir directamente Cliente con Producto sin pasar por las relaciones intermedias;
* olvidar la relación ​**LineaPedido**​, que actúa como nexo entre pedidos y productos;
* utilizar atributos incorrectos en las condiciones de JOIN;
* proyectar atributos antes de completar todos los JOIN necesarios;
* confundir el producto cartesiano con el JOIN.

Durante la corrección conviene recordar una regla sencilla que será útil durante todo el curso:

> **Antes de escribir un JOIN, identifica siempre el camino que sigue la información entre las relaciones.**

Cuando el estudiante visualiza correctamente ese recorrido, la construcción de la consulta resulta mucho más sencilla y los errores disminuyen considerablemente.

