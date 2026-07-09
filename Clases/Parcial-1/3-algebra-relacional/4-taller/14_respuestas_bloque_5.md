# Soluciones guiadas — Bloque 5. Optimización de consultas en Álgebra Relacional

## Introducción

Hasta este punto del taller el objetivo consistía en obtener el resultado correcto.

En este bloque aparece un aspecto fundamental en cualquier sistema gestor de bases de datos: ​**la optimización de consultas**​.

Dos expresiones de Álgebra Relacional pueden producir exactamente el mismo resultado y, sin embargo, requerir tiempos de ejecución completamente distintos.

El objetivo del optimizador es transformar una expresión algebraica en otra equivalente, pero que necesite menos operaciones, procese menos tuplas y reduzca el coste total de ejecución.

En estos ejercicios el estudiante no debe modificar el resultado de la consulta, sino encontrar una forma más eficiente de obtenerlo.

---

# Ejercicio 1

### Enunciado

Se desea obtener el nombre de los clientes de Santander que han realizado pedidos.

Un estudiante propone la siguiente solución:

```text
R1 ← Cliente ⋈ Cliente.IdCliente = Pedido.IdCliente Pedido

R2 ← σ Ciudad='Santander' (R1)

R3 ← π Nombre (R2)

Resultado ← R3
```

Reescribe la consulta aplicando una estrategia más eficiente.

### Solución

```text
R1 ← σ Ciudad='Santander' (Cliente)

R2 ← R1 ⋈ R1.IdCliente = Pedido.IdCliente Pedido

R3 ← π Nombre (R2)

Resultado ← R3
```

### Explicación

La selección debe realizarse antes del JOIN.

De este modo el JOIN trabaja únicamente con los clientes de Santander y no con toda la relación Cliente.

---

# Ejercicio 2

### Enunciado

Un estudiante escribe:

```text
R1 ← Cliente ⋈ Pedido

R2 ← Pedido ⋈ LineaPedido

R3 ← LineaPedido ⋈ Producto

R4 ← σ Precio > 500 (R3)

Resultado ← π Producto.Nombre (R4)
```

Reordena las operaciones para reducir el número de tuplas procesadas.

### Solución

```text
R1 ← σ Precio > 500 (Producto)

R2 ← R1 ⋈ R1.IdProducto = LineaPedido.IdProducto LineaPedido

R3 ← R2 ⋈ LineaPedido.IdPedido = Pedido.IdPedido Pedido

R4 ← R3 ⋈ Pedido.IdCliente = Cliente.IdCliente Cliente

R5 ← π Producto.Nombre (R4)

Resultado ← R5
```

### Explicación

Filtrar primero los productos caros reduce considerablemente el tamaño de todas las relaciones posteriores.

---

# Ejercicio 3

### Enunciado

Explica por qué las selecciones deben aplicarse tan pronto como sea posible.

### Solución

No requiere construir una consulta nueva.

La idea puede resumirse mediante la siguiente transformación.

```text
R1 ← R ⋈ S

R2 ← σ condición (R1)
```

↓

```text
R1 ← σ condición (R)

R2 ← R1 ⋈ S
```

### Explicación

Ambas expresiones producen el mismo resultado.

Sin embargo, la segunda procesa menos registros durante el JOIN y, por tanto, resulta más eficiente.

---

# Ejercicio 4

### Enunciado

Se desea obtener únicamente el nombre de los productos vendidos.

Un estudiante mantiene todos los atributos durante toda la consulta.

¿Cómo podría optimizarse?

### Solución

```text
R1 ← π IdProducto, Nombre (Producto)

R2 ← R1 ⋈ R1.IdProducto = LineaPedido.IdProducto LineaPedido

R3 ← π Nombre (R2)

Resultado ← R3
```

### Explicación

La primera proyección elimina columnas innecesarias antes del JOIN.

Al reducir el ancho de las tuplas también disminuye el coste de procesamiento.

---

# Ejercicio 5

### Enunciado

Indica cuál de las siguientes estrategias es más eficiente.

Opción A

```text
Cliente

↓

JOIN Pedido

↓

Selección
```

Opción B

```text
Selección Cliente

↓

JOIN Pedido
```

### Solución

La opción correcta es la ​**B**​.

Representación:

```text
R1 ← σ condición (Cliente)

R2 ← R1 ⋈ Pedido

Resultado ← R2
```

### Explicación

Siempre que la condición afecte únicamente a Cliente, la selección debe ejecutarse antes del JOIN.

---

# Ejercicio 6

### Enunciado

Explica qué ocurre cuando una proyección elimina un atributo que posteriormente será necesario para realizar un JOIN.

### Solución

Ejemplo incorrecto:

```text
R1 ← π Nombre (Cliente)

R2 ← R1 ⋈ Pedido
```

### Explicación

La consulta ya no puede ejecutarse porque se ha eliminado ​**IdCliente**​, atributo necesario para relacionar ambas tablas.

Una proyección solo debe realizarse cuando ya no vaya a necesitarse la información eliminada.

---

# Ejercicio 7

### Enunciado

La empresa desea obtener los productos de la categoría Monitores vendidos en pedidos realizados por clientes de Santander.

Escribe una versión optimizada.

### Solución

```text
R1 ← σ Ciudad='Santander' (Cliente)

R2 ← σ Categoria='Monitores' (Producto)

R3 ← R1 ⋈ R1.IdCliente = Pedido.IdCliente Pedido

R4 ← R3 ⋈ Pedido.IdPedido = LineaPedido.IdPedido LineaPedido

R5 ← R4 ⋈ LineaPedido.IdProducto = R2.IdProducto R2

R6 ← π R2.Nombre (R5)

Resultado ← R6
```

### Explicación

Las dos selecciones se realizan antes de cualquier JOIN.

Esto reduce drásticamente el volumen de datos procesados.

---

# Ejercicio 8

### Enunciado

Resume las tres reglas básicas de optimización aprendidas en este bloque.

### Solución

```text
Aplicar las selecciones lo antes posible.
```

```text
Realizar las proyecciones cuando ya no sean necesarios los atributos eliminados.
```

```text
Reducir el tamaño de las relaciones antes de ejecutar los JOIN.
```

### Explicación

Estas tres reglas constituyen la base de la mayoría de los optimizadores de consultas utilizados por los SGBD modernos.

---

# Observaciones para la corrección

En este bloque no se evalúa únicamente si el resultado es correcto.

También debe valorarse la estrategia utilizada para construir la consulta.

Los errores más habituales son:

* aplicar las selecciones después de todos los JOIN;
* proyectar demasiado pronto y eliminar atributos necesarios;
* pensar que cualquier expresión equivalente tiene el mismo coste;
* no justificar por qué una versión resulta más eficiente que otra.

Es importante transmitir al estudiante que ​**optimizar una consulta no significa cambiar su resultado**​, sino obtener exactamente la misma información realizando un menor trabajo.

