# Producto cartesiano y CROSS JOIN

## Introducción

De todos los operadores estudiados en el Álgebra Relacional, el **producto cartesiano (×)** suele ser el que más dudas genera entre los estudiantes. A primera vista parece una operación poco útil, ya que produce un número muy elevado de tuplas y, en la mayoría de los casos, los resultados obtenidos no tienen significado práctico.

Sin embargo, esta impresión es engañosa.

El producto cartesiano constituye uno de los pilares del Modelo Relacional y desempeña un papel fundamental en la construcción de operaciones más complejas. De hecho, el operador ​**JOIN**​, ampliamente utilizado en SQL, puede entenderse como un producto cartesiano seguido de una selección que conserva únicamente las combinaciones válidas.

Por ello, antes de estudiar los distintos tipos de JOIN es imprescindible comprender qué hace realmente el producto cartesiano y por qué SQL incorpora la cláusula ​**CROSS JOIN**​.

### ¿Qué es un producto cartesiano?

En matemáticas, el producto cartesiano de dos conjuntos consiste en generar todas las combinaciones posibles entre los elementos del primer conjunto y los del segundo.

El Álgebra Relacional aplica exactamente la misma idea sobre relaciones.

Si disponemos de las siguientes relaciones:

**Cliente**

| IdCliente | Nombre      |
| ----------: | ------------- |
|         1 | Ana Ruiz    |
|         2 | Luis Pérez |

**Almacen**

| IdAlmacen | Ciudad    |
| ----------: | ----------- |
|         1 | Santander |
|         2 | Bilbao    |
|         3 | Oviedo    |

El producto cartesiano se expresa como:

```text
Cliente × Almacen
```

El resultado contiene todas las combinaciones posibles entre clientes y almacenes.

| Cliente     | Almacén  |
| ------------- | ----------- |
| Ana Ruiz    | Santander |
| Ana Ruiz    | Bilbao    |
| Ana Ruiz    | Oviedo    |
| Luis Pérez | Santander |
| Luis Pérez | Bilbao    |
| Luis Pérez | Oviedo    |

Puede observarse que el número de filas del resultado es:

> **Número de filas de la primera relación × Número de filas de la segunda relación**

En este ejemplo:

* Cliente: 2 filas.
* Almacén: 3 filas.

Resultado:

2 × 3 = ​**6 filas**​.

Esta propiedad se mantiene siempre, independientemente del tamaño de las relaciones.

### ¿Cómo se representa en SQL?

La traducción directa es la cláusula ​**CROSS JOIN**​.

```sql
SELECT *
FROM Cliente
CROSS JOIN Almacen;
```

El resultado es exactamente el mismo que el obtenido mediante el operador ×.

En otras palabras:

| Álgebra Relacional | SQL        |
| --------------------- | ------------ |
| ×                  | CROSS JOIN |

La correspondencia es directa.

### ¿Por qué casi nunca vemos CROSS JOIN en aplicaciones reales?

La respuesta es sencilla.

En la mayoría de los problemas reales no interesa combinar todos los registros de ambas tablas.

Supongamos que una empresa tiene:

* 10 000 clientes.
* 200 productos.

Un producto cartesiano produciría:

10 000 × 200 = ​**2 000 000 filas**​.

La inmensa mayoría de esas combinaciones no representan ninguna relación existente entre clientes y productos.

Por tanto, el resultado carece de utilidad práctica y supondría un enorme coste computacional.

### Del producto cartesiano al JOIN

Aquí aparece una de las ideas más importantes del curso.

Supongamos las relaciones:

**Cliente**

| IdCliente | Nombre      |
| ----------: | ------------- |
|         1 | Ana Ruiz    |
|         2 | Luis Pérez |

**Pedido**

| IdPedido | IdCliente |
| ---------: | ----------: |
|      101 |         1 |
|      102 |         1 |
|      103 |         2 |

Podríamos construir el siguiente producto cartesiano:

```text
Cliente × Pedido
```

El resultado contendría:

| Cliente     | Pedido |
| ------------- | -------- |
| Ana Ruiz    | 101    |
| Ana Ruiz    | 102    |
| Ana Ruiz    | 103    |
| Luis Pérez | 101    |
| Luis Pérez | 102    |
| Luis Pérez | 103    |

Sin embargo, solo algunas combinaciones son correctas.

Si aplicamos una selección:

```text
σ Cliente.IdCliente = Pedido.IdCliente
(
Cliente × Pedido
)
```

Obtendremos únicamente las relaciones válidas.

Este proceso equivale exactamente a un JOIN.

Por ello suele afirmarse que:

> **JOIN = Producto cartesiano + Selección**

Esta definición será la base del siguiente capítulo.

### SQL moderno y CROSS JOIN implícito

En las primeras versiones de SQL era frecuente escribir consultas como:

```sql
SELECT *
FROM Cliente, Pedido;
```

Esta sintaxis generaba inicialmente un producto cartesiano implícito.

Posteriormente, la cláusula WHERE eliminaba las combinaciones incorrectas.

```sql
SELECT *
FROM Cliente, Pedido
WHERE Cliente.IdCliente = Pedido.IdCliente;
```

Aunque esta sintaxis sigue siendo válida en muchos SGBD, actualmente se recomienda utilizar la sintaxis explícita basada en JOIN, ya que resulta mucho más legible y evita errores.

### Casos reales

Existen situaciones donde un CROSS JOIN sí resulta útil.

Por ejemplo:

* generar todas las combinaciones posibles entre colores y tallas de un producto;
* crear calendarios combinando días y franjas horarias;
* construir escenarios de simulación;
* realizar pruebas automáticas sobre conjuntos de parámetros.

En estos casos el objetivo es precisamente obtener todas las combinaciones posibles.

### Errores frecuentes

El error más habitual consiste en olvidar la condición de unión después de generar un producto cartesiano.

En SQL esto produce una enorme cantidad de filas aparentemente "duplicadas", cuando en realidad todas las combinaciones son correctas desde el punto de vista del producto cartesiano.

Otro error frecuente consiste en utilizar CROSS JOIN cuando realmente se necesita un INNER JOIN.

Esta confusión suele provocar consultas muy lentas y resultados completamente incorrectos.

### Ideas clave

* El producto cartesiano genera todas las combinaciones posibles entre dos relaciones.
* El número de filas del resultado es el producto del número de filas de ambas relaciones.
* En SQL, el operador equivalente es ​**CROSS JOIN**​.
* El producto cartesiano rara vez se utiliza de forma aislada en aplicaciones reales.
* Un JOIN puede entenderse como un producto cartesiano seguido de una selección.
* Comprender esta relación facilita enormemente el estudio de los distintos tipos de JOIN en SQL.

