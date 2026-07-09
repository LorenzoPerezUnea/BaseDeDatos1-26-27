# Soluciones guiadas — Bloque 4. Consultas encadenadas

## Introducción

En este bloque el estudiante debe combinar prácticamente todos los operadores estudiados hasta el momento.

Ya no basta con conocer la sintaxis de cada operación. Ahora es necesario desarrollar una estrategia de resolución, identificando el recorrido que debe seguir la información entre las distintas relaciones.

Una recomendación que se mantendrá durante todo el curso es la siguiente:

1. Identificar qué información solicita el enunciado.
2. Localizar en qué relaciones se encuentra esa información.
3. Aplicar las selecciones lo antes posible.
4. Construir los JOIN siguiendo el recorrido natural del modelo.
5. Proyectar únicamente los atributos solicitados.
6. Asignar el resultado final.

Esta forma de trabajar es muy similar a la utilizada posteriormente durante el diseño de consultas SQL y facilita enormemente la corrección y depuración de errores.

Durante este bloque se utilizarán las relaciones:

* Cliente(IdCliente, Nombre, Ciudad)
* Pedido(IdPedido, IdCliente, Fecha)
* LineaPedido(IdPedido, IdProducto, Cantidad)
* Producto(IdProducto, Nombre, Categoria, Precio)

---

# Ejercicio 1

### Enunciado

Obtener el nombre de los clientes de Santander que han realizado algún pedido.

### Solución

```text
R1 ← σ Ciudad='Santander' (Cliente)

R2 ← R1 ⋈ R1.IdCliente = Pedido.IdCliente Pedido

R3 ← π Nombre (R2)

Resultado ← R3
```

### Explicación

La selección se realiza sobre la relación ​**Cliente**​, ya que el atributo **Ciudad** pertenece a dicha relación.

Una vez reducido el conjunto de clientes, se realiza el JOIN con **Pedido** para obtener únicamente aquellos clientes que han realizado al menos un pedido.

Finalmente se proyecta el nombre.

---

# Ejercicio 2

### Enunciado

Mostrar el nombre y el precio de todos los productos vendidos durante el pedido 1003.

### Solución

```text
R1 ← σ IdPedido = 1003 (Pedido)

R2 ← R1 ⋈ R1.IdPedido = LineaPedido.IdPedido LineaPedido

R3 ← R2 ⋈ LineaPedido.IdProducto = Producto.IdProducto Producto

R4 ← π Producto.Nombre, Producto.Precio (R3)

Resultado ← R4
```

### Explicación

El recorrido lógico es:

Pedido

→ LineaPedido

→ Producto

Filtrar el pedido desde el primer paso reduce significativamente el número de registros procesados.

---

# Ejercicio 3

### Enunciado

Obtener el nombre de los clientes que han comprado productos pertenecientes a la categoría ​**Periféricos**​.

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

Comenzar por la relación **Producto** resulta más eficiente que comenzar por ​**Cliente**​, ya que la selección inicial elimina gran parte de las tuplas antes de realizar los JOIN.

---

# Ejercicio 4

### Enunciado

Mostrar los nombres de los productos comprados por clientes residentes en Bilbao.

### Solución

```text
R1 ← σ Ciudad='Bilbao' (Cliente)

R2 ← R1 ⋈ R1.IdCliente = Pedido.IdCliente Pedido

R3 ← R2 ⋈ Pedido.IdPedido = LineaPedido.IdPedido LineaPedido

R4 ← R3 ⋈ LineaPedido.IdProducto = Producto.IdProducto Producto

R5 ← π Producto.Nombre (R4)

Resultado ← R5
```

### Explicación

El recorrido parte de los clientes porque la condición del problema afecta a la ciudad de residencia.

---

# Ejercicio 5

### Enunciado

La dirección comercial desea conocer los nombres de los clientes que han realizado pedidos posteriores al 5 de marzo de 2025.

### Solución

```text
R1 ← σ Fecha > '2025-03-05' (Pedido)

R2 ← R1 ⋈ R1.IdCliente = Cliente.IdCliente Cliente

R3 ← π Cliente.Nombre (R2)

Resultado ← R3
```

### Explicación

En este ejercicio la selección debe realizarse sobre ​**Pedido**​, ya que el atributo **Fecha** pertenece a esa relación.

---

# Ejercicio 6

### Enunciado

Obtener el nombre de todos los productos cuyo precio sea superior a 150 € y que además hayan sido vendidos al menos una vez.

### Solución

```text
R1 ← σ Precio > 150 (Producto)

R2 ← R1 ⋈ R1.IdProducto = LineaPedido.IdProducto LineaPedido

R3 ← π Producto.Nombre (R2)

Resultado ← R3
```

### Explicación

El JOIN garantiza que únicamente aparecen productos presentes en alguna línea de pedido.

La selección reduce previamente el catálogo.

---

# Ejercicio 7

### Enunciado

Mostrar el nombre de los clientes que han comprado un ​**SSD 1 TB**​.

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

La estrategia consiste en localizar primero el producto y recorrer posteriormente las relaciones hasta llegar al cliente.

---

# Ejercicio 8

### Enunciado

Obtener el nombre de los clientes y los productos que aparecen en cada uno de sus pedidos.

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

Como no existe ninguna condición de filtrado, la consulta consiste únicamente en recorrer correctamente las cuatro relaciones.

---

# Ejercicio 9

### Enunciado

La empresa desea conocer todos los productos vendidos a clientes de Santander cuyo precio sea inferior a 100 €.

### Solución

```text
R1 ← σ Ciudad='Santander' (Cliente)

R2 ← σ Precio < 100 (Producto)

R3 ← R1 ⋈ R1.IdCliente = Pedido.IdCliente Pedido

R4 ← R3 ⋈ Pedido.IdPedido = LineaPedido.IdPedido LineaPedido

R5 ← R4 ⋈ LineaPedido.IdProducto = R2.IdProducto R2

R6 ← π R2.Nombre (R5)

Resultado ← R6
```

### Explicación

Este ejercicio ilustra una técnica muy recomendable: aplicar selecciones independientes sobre distintas relaciones antes de comenzar los JOIN.

De este modo se trabaja siempre con conjuntos de datos más pequeños.

---

# Ejercicio 10

### Enunciado

Mostrar el nombre de los clientes que hayan comprado simultáneamente un **Monitor 27"** y un ​**Ratón Inalámbrico**​.

### Solución

```text
R1 ← σ Nombre='Monitor 27"' (Producto)

R2 ← R1 ⋈ R1.IdProducto = LineaPedido.IdProducto LineaPedido

R3 ← R2 ⋈ LineaPedido.IdPedido = Pedido.IdPedido Pedido

R4 ← π IdCliente (R3)


R5 ← σ Nombre='Ratón Inalámbrico' (Producto)

R6 ← R5 ⋈ R5.IdProducto = LineaPedido.IdProducto LineaPedido

R7 ← R6 ⋈ LineaPedido.IdPedido = Pedido.IdPedido Pedido

R8 ← π IdCliente (R7)


R9 ← R4 ∩ R8


R10 ← R9 ⋈ R9.IdCliente = Cliente.IdCliente Cliente

R11 ← π Nombre (R10)

Resultado ← R11
```

### Explicación

Este es uno de los ejercicios más completos del taller.

Combina:

* selección;
* proyección;
* JOIN;
* intersección.

El estudiante debe comprender que el problema se resuelve obteniendo primero dos conjuntos independientes de clientes y calculando posteriormente su intersección.

---

# Ejercicio 11

### Enunciado

La empresa desea localizar los clientes registrados que todavía no han realizado ningún pedido.

### Solución

```text
R1 ← π IdCliente (Cliente)

R2 ← π IdCliente (Pedido)

R3 ← R1 − R2

R4 ← R3 ⋈ R3.IdCliente = Cliente.IdCliente Cliente

R5 ← π Nombre (R4)

Resultado ← R5
```

### Explicación

Este ejercicio reutiliza el operador diferencia estudiado en el bloque anterior y demuestra cómo combinar operaciones de conjuntos con JOIN.

---

# Ejercicio 12

### Enunciado

La dirección comercial desea generar un informe con:

* nombre del cliente;
* nombre del producto;
* cantidad comprada;
* precio del producto.

### Solución

```text
R1 ← Cliente ⋈ Cliente.IdCliente = Pedido.IdCliente Pedido

R2 ← R1 ⋈ Pedido.IdPedido = LineaPedido.IdPedido LineaPedido

R3 ← R2 ⋈ LineaPedido.IdProducto = Producto.IdProducto Producto

R4 ← π Cliente.Nombre,
         Producto.Nombre,
         LineaPedido.Cantidad,
         Producto.Precio
     (R3)

Resultado ← R4
```

### Explicación

La consulta combina las cuatro relaciones principales del modelo.

No es necesaria ninguna selección porque el enunciado solicita toda la información disponible sobre las ventas.

---

# Observaciones para la corrección

Este bloque representa el primer contacto del estudiante con consultas de complejidad media.

Los errores más habituales son:

* no identificar correctamente el recorrido entre las relaciones;
* comenzar la consulta sin planificar una estrategia;
* aplicar la selección sobre una relación incorrecta;
* realizar la proyección demasiado pronto, eliminando atributos necesarios para los JOIN posteriores;
* olvidar alguna relación intermedia, especialmente ​**LineaPedido**​.

Durante la corrección conviene insistir en una idea que acompañará al estudiante durante todo el resto del curso:

> **Una consulta compleja no se escribe de una vez; se construye paso a paso.**

La utilización de relaciones intermedias (`R1`, `R2`, `R3`, ...) no solo mejora la legibilidad, sino que también facilita la depuración de errores, la asignación de puntuación parcial y la posterior traducción de la consulta al lenguaje SQL.

