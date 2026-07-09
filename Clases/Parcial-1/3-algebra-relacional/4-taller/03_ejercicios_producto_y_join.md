# Ejercicios de producto cartesiano y JOIN

## Introducción

En el bloque anterior todas las consultas podían resolverse utilizando una única relación.

A partir de este momento eso dejará de ser suficiente.

En una base de datos real, la información suele encontrarse repartida entre varias relaciones. Para responder a una pregunta será necesario combinar datos procedentes de distintas tablas.

El objetivo de este bloque es aprender a identificar cuándo una consulta necesita información distribuida en varias relaciones y comprender el papel del producto cartesiano como base matemática del JOIN.

En la práctica profesional rara vez se utiliza un producto cartesiano de forma aislada. Sin embargo, comprender su funcionamiento resulta imprescindible para entender el origen del JOIN y para evitar uno de los errores más frecuentes al escribir consultas: combinar relaciones sin establecer correctamente la condición de unión.

Durante este bloque se trabajará con las cuatro relaciones del dataset:

* Cliente
* Pedido
* Producto
* LineaPedido

No es necesario escribir SQL.

Todas las respuestas deberán expresarse utilizando únicamente operadores del Álgebra Relacional.

---

## Ejercicio 1

### Enunciado

La dirección comercial desea conocer el nombre de todos los clientes que han realizado algún pedido.

### Reflexiona antes de comenzar

* ¿La información se encuentra en una sola relación?
* ¿Qué relación contiene el nombre del cliente?
* ¿Qué relación indica quién ha realizado cada pedido?

Espacio para la solución:

..........................................................................

..........................................................................

---

## Ejercicio 2

### Enunciado

Obtener el identificador de todos los pedidos realizados por clientes de Santander.

### Pistas

Será necesario:

* localizar primero a los clientes;
* relacionarlos con sus pedidos.

Espacio para la solución:

..........................................................................

..........................................................................

---

## Ejercicio 3

### Enunciado

Mostrar el nombre de los productos incluidos en el pedido ​**1003**​.

### Reflexiona

¿Es suficiente con utilizar únicamente la relación Producto?

¿Dónde aparece la relación entre un pedido y un producto?

Espacio para la solución:

..........................................................................

..........................................................................

---

## Ejercicio 4

### Enunciado

Obtener el nombre de los clientes que han comprado un producto de la categoría ​**Periféricos**​.

### Observación

Por primera vez será necesario recorrer varias relaciones.

Intenta identificar el camino antes de escribir la expresión.

Espacio para la solución:

..........................................................................

..........................................................................

---

## Ejercicio 5

### Enunciado

Mostrar el nombre y la cantidad de todos los productos vendidos en el pedido ​**1001**​.

Espacio para la solución:

..........................................................................

..........................................................................

---

## Ejercicio 6

### Enunciado

La empresa desea conocer todos los pedidos realizados por clientes de Bilbao.

Indica primero el orden lógico de las operaciones y, posteriormente, escribe la expresión algebraica.

Espacio para la solución:

..........................................................................

..........................................................................

---

## Ejercicio 7

### Enunciado

¿Qué ocurriría si realizáramos un producto cartesiano entre las relaciones Cliente y Producto sin aplicar posteriormente ninguna condición de selección?

No es necesario escribir una expresión.

Explica brevemente el resultado obtenido.

Espacio para la respuesta:

..........................................................................

..........................................................................

..........................................................................

---

## Ejercicio 8

### Enunciado

Calcular cuántas tuplas produciría el producto cartesiano entre las relaciones Cliente y Producto del dataset proporcionado.

No es necesario escribir la relación completa.

Razona únicamente el número de tuplas resultantes.

Espacio para la solución:

..........................................................................

..........................................................................

---

## Ejercicio 9

### Enunciado

Obtener el nombre de los clientes que compraron el producto ​**SSD 1 TB**​.

### Consejo

Empieza localizando el producto y sigue el recorrido inverso hasta llegar al cliente.

Espacio para la solución:

..........................................................................

..........................................................................

---

## Ejercicio 10

### Enunciado

La empresa desea elaborar un listado que muestre:

* nombre del cliente;
* nombre del producto;
* cantidad comprada.

No es necesario filtrar ningún pedido.

¿Qué relaciones intervienen?

¿En qué orden realizarías los JOIN?

Espacio para la solución:

..........................................................................

..........................................................................

..........................................................................

---

## Ejercicio 11

### Enunciado

Explica con tus propias palabras por qué el JOIN puede entenderse como un producto cartesiano seguido de una selección.

No escribas símbolos algebraicos.

Describe únicamente el razonamiento.

Espacio para la respuesta:

..........................................................................

..........................................................................

..........................................................................

..........................................................................

---

## Ejercicio 12

### Enunciado

Observa la siguiente secuencia de operadores.

```text
Cliente

↓

JOIN Pedido

↓

JOIN LineaPedido

↓

JOIN Producto

↓

Proyección (NombreCliente, NombreProducto)
```

Responde:

* ¿Qué información devolvería esta consulta?
* ¿Qué operador elimina los atributos innecesarios?
* ¿Qué operador permite combinar las cuatro relaciones?

Espacio para la respuesta:

..........................................................................

..........................................................................

..........................................................................

..........................................................................

---

## Ejercicio de reflexión

Antes de continuar con el siguiente bloque, responde mentalmente a las siguientes preguntas.

* ¿Cuándo basta con una selección?
* ¿Cuándo es necesario utilizar un JOIN?
* ¿Qué problema resuelve el producto cartesiano?
* ¿Por qué un JOIN necesita una condición de unión?
* ¿Cómo identificar rápidamente las relaciones que intervienen en una consulta?

Si eres capaz de responder con seguridad a estas preguntas, estás preparado para comenzar a trabajar con operaciones entre conjuntos.

---

## Ideas clave

* El JOIN permite combinar información distribuida entre varias relaciones.
* Conceptualmente, un JOIN puede interpretarse como un producto cartesiano seguido de una selección.
* Antes de escribir una consulta conviene identificar el recorrido que sigue la información entre las relaciones.
* El producto cartesiano, utilizado de forma aislada, genera combinaciones que normalmente no tienen significado práctico.
* Comprender el camino entre las relaciones facilita enormemente la resolución de consultas complejas.

