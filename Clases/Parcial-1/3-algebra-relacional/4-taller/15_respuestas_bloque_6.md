# Soluciones guiadas — Bloque 6. Consulta integradora del caso práctico

## Introducción

Este último bloque integra todos los conocimientos desarrollados durante el taller.

A diferencia de los bloques anteriores, donde cada ejercicio estaba orientado a practicar un operador o una técnica concreta, aquí el estudiante debe enfrentarse a una consulta completa similar a las que aparecen en un entorno profesional.

No existe un único camino para resolver estos ejercicios. Es posible obtener el mismo resultado utilizando estrategias ligeramente diferentes. Durante la corrección deberá valorarse principalmente:

* que el recorrido entre las relaciones sea correcto;
* que las selecciones se apliquen sobre la relación adecuada;
* que los JOIN estén correctamente definidos;
* que la proyección final contenga únicamente los atributos solicitados;
* que la estrategia sea razonablemente eficiente.

En todos los ejercicios se utilizará el modelo de la empresa trabajado durante todo el curso.

---

# Ejercicio 1

### Enunciado

La dirección comercial desea obtener un listado con el nombre de los clientes de **Santander** que hayan comprado algún producto de la categoría ​**Monitores**​.

### Solución

```text
R1 ← σ Ciudad = 'Santander' (Cliente)

R2 ← σ Categoria = 'Monitores' (Producto)

R3 ← R1 ⋈ R1.IdCliente = Pedido.IdCliente Pedido

R4 ← R3 ⋈ Pedido.IdPedido = LineaPedido.IdPedido LineaPedido

R5 ← R4 ⋈ LineaPedido.IdProducto = R2.IdProducto R2

R6 ← π R1.Nombre (R5)

Resultado ← R6
```

### Explicación

Las dos selecciones se realizan al comienzo para reducir el número de registros que participarán en los JOIN posteriores.

---

# Ejercicio 2

### Enunciado

Obtener el nombre de todos los clientes que hayan comprado un producto cuyo precio sea superior a ​**500 €**​.

### Solución

```text
R1 ← σ Precio > 500 (Producto)

R2 ← R1 ⋈ R1.IdProducto = LineaPedido.IdProducto LineaPedido

R3 ← R2 ⋈ LineaPedido.IdPedido = Pedido.IdPedido Pedido

R4 ← R3 ⋈ Pedido.IdCliente = Cliente.IdCliente Cliente

R5 ← π Cliente.Nombre (R4)

Resultado ← R5
```

### Explicación

El recorrido comienza en Producto porque la condición afecta al precio.

---

# Ejercicio 3

### Enunciado

Obtener el nombre de los clientes que han realizado pedidos pero nunca han comprado un producto de la categoría ​**Accesorios**​.

### Solución

Primero se obtienen todos los clientes con pedidos.

```text
R1 ← Cliente ⋈ Cliente.IdCliente = Pedido.IdCliente Pedido

R2 ← π Cliente.IdCliente (R1)
```

Después se obtienen los clientes que sí compraron accesorios.

```text
R3 ← σ Categoria = 'Accesorios' (Producto)

R4 ← R3 ⋈ R3.IdProducto = LineaPedido.IdProducto LineaPedido

R5 ← R4 ⋈ LineaPedido.IdPedido = Pedido.IdPedido Pedido

R6 ← π IdCliente (R5)
```

Se calcula la diferencia.

```text
R7 ← R2 − R6
```

Finalmente se recuperan los nombres.

```text
R8 ← R7 ⋈ R7.IdCliente = Cliente.IdCliente Cliente

R9 ← π Nombre (R8)

Resultado ← R9
```

### Explicación

Este ejercicio combina JOIN, proyección, selección y diferencia.

Es una consulta muy representativa de problemas reales.

---

# Ejercicio 4

### Enunciado

La empresa desea conocer los productos vendidos tanto a clientes de Santander como a clientes de Bilbao.

### Solución

Clientes de Santander.

```text
R1 ← σ Ciudad = 'Santander' (Cliente)

R2 ← R1 ⋈ R1.IdCliente = Pedido.IdCliente Pedido

R3 ← R2 ⋈ Pedido.IdPedido = LineaPedido.IdPedido LineaPedido

R4 ← π IdProducto (R3)
```

Clientes de Bilbao.

```text
R5 ← σ Ciudad = 'Bilbao' (Cliente)

R6 ← R5 ⋈ R5.IdCliente = Pedido.IdCliente Pedido

R7 ← R6 ⋈ Pedido.IdPedido = LineaPedido.IdPedido LineaPedido

R8 ← π IdProducto (R7)
```

Intersección.

```text
R9 ← R4 ∩ R8
```

Recuperación de los nombres.

```text
R10 ← R9 ⋈ R9.IdProducto = Producto.IdProducto Producto

R11 ← π Nombre (R10)

Resultado ← R11
```

### Explicación

La intersección permite localizar los productos comunes a ambos conjuntos de ventas.

---

# Ejercicio 5

### Enunciado

Obtener un informe con:

* nombre del cliente;
* nombre del producto;
* cantidad;
* precio;
* importe total de la línea.

### Solución

```text
R1 ← Cliente ⋈ Cliente.IdCliente = Pedido.IdCliente Pedido

R2 ← R1 ⋈ Pedido.IdPedido = LineaPedido.IdPedido LineaPedido

R3 ← R2 ⋈ LineaPedido.IdProducto = Producto.IdProducto Producto

R4 ← π Cliente.Nombre,
         Producto.Nombre,
         Cantidad,
         Precio,
         (Cantidad × Precio) → Importe
     (R3)

Resultado ← R4
```

### Explicación

La operación `(Cantidad × Precio)` representa un atributo calculado.

Aunque el Álgebra Relacional clásica no incorpora formalmente operaciones aritméticas, esta notación resulta útil desde un punto de vista didáctico y facilita la transición hacia SQL.

---

# Ejercicio 6

### Enunciado

Construye una estrategia de resolución para responder a la siguiente consulta:

> "Obtener los nombres de los clientes de Santander que hayan comprado un Monitor 27'' con un precio superior a 300 €."

### Solución

```text
R1 ← σ Ciudad = 'Santander' (Cliente)

R2 ← σ Nombre = 'Monitor 27"' ∧ Precio > 300 (Producto)

R3 ← R1 ⋈ R1.IdCliente = Pedido.IdCliente Pedido

R4 ← R3 ⋈ Pedido.IdPedido = LineaPedido.IdPedido LineaPedido

R5 ← R4 ⋈ LineaPedido.IdProducto = R2.IdProducto R2

R6 ← π R1.Nombre (R5)

Resultado ← R6
```

### Explicación

Esta solución resume prácticamente todo lo aprendido durante el taller:

* selección sobre varias relaciones;
* múltiples JOIN;
* planificación del recorrido;
* optimización mediante selecciones tempranas;
* proyección final.

---

# Observaciones para la corrección

Este bloque debe considerarse una evaluación integradora del taller.

No debe penalizarse una estrategia alternativa siempre que:

* produzca exactamente el mismo resultado;
* utilice correctamente los operadores del Álgebra Relacional;
* mantenga la coherencia entre las relaciones;
* conserve los atributos necesarios para los JOIN;
* finalice con una proyección adecuada.

Los errores que deberían penalizarse con mayor severidad son:

* utilizar claves incorrectas en los JOIN;
* omitir relaciones intermedias, especialmente ​**LineaPedido**​;
* proyectar antes de completar los JOIN necesarios;
* aplicar condiciones sobre atributos pertenecientes a otra relación;
* confundir operaciones de conjuntos con condiciones de selección.

Como cierre del taller, es recomendable insistir en que el estudiante ha seguido el mismo proceso que realiza internamente un SGBD moderno:

1. Interpretar una necesidad de información.
2. Traducirla a una expresión de Álgebra Relacional.
3. Optimizar la estrategia de ejecución.
4. Obtener el conjunto de resultados esperado.

Este razonamiento servirá como puente natural hacia la siguiente clase, donde esas mismas consultas se expresarán utilizando ​**SQL**​, comprobando que el lenguaje declarativo no sustituye al Álgebra Relacional, sino que se apoya directamente en ella como fundamento teórico.

