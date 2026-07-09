# Ejercicios de selección y proyección

## Introducción

Comenzaremos el taller utilizando únicamente los dos operadores más sencillos y, al mismo tiempo, los más utilizados de todo el Álgebra Relacional:

* ​**Selección (σ)**​, para filtrar tuplas.
* ​**Proyección (π)**​, para seleccionar atributos.

Aunque estos ejercicios puedan parecer simples, es importante resolverlos con rigor.

En la mayoría de las consultas reales, incluso las más complejas, la primera operación suele consistir en reducir el volumen de información mediante una selección y, posteriormente, eliminar los atributos innecesarios mediante una proyección.

Por este motivo es fundamental dominar estos operadores antes de pasar al estudio de consultas que involucren varias relaciones.

En todos los ejercicios de este bloque ​**solo se permite utilizar las relaciones Cliente y Producto**​.

No será necesario utilizar JOIN ni ningún otro operador.

---

## Ejercicio 1

### Enunciado

Obtener **todos los datos** de los clientes cuya ciudad sea ​**Santander**​.

### Pistas

* Solo interviene una relación.
* No es necesario eliminar atributos.
* Piensa qué operador permite filtrar filas.

Espacio para la solución:

..........................................................................

..........................................................................

---

## Ejercicio 2

### Enunciado

Obtener únicamente el **nombre** de todos los clientes.

### Pistas

* No existe ningún filtro.
* Solo interesa un atributo.

Espacio para la solución:

..........................................................................

..........................................................................

---

## Ejercicio 3

### Enunciado

Obtener el **nombre** y la **ciudad** de los clientes de Bilbao.

### Pistas

* Será necesario combinar dos operadores.
* Piensa cuál debe aplicarse primero.

Espacio para la solución:

..........................................................................

..........................................................................

---

## Ejercicio 4

### Enunciado

Mostrar todos los productos cuyo precio sea superior a ​**200 euros**​.

Espacio para la solución:

..........................................................................

..........................................................................

---

## Ejercicio 5

### Enunciado

Obtener únicamente el **nombre** de todos los productos de la categoría ​**Periféricos**​.

Espacio para la solución:

..........................................................................

..........................................................................

---

## Ejercicio 6

### Enunciado

Mostrar el nombre y el precio de todos los productos cuyo precio sea inferior a ​**100 euros**​.

Espacio para la solución:

..........................................................................

..........................................................................

---

## Ejercicio 7

### Enunciado

Obtener el listado de categorías existentes en el catálogo de productos.

### Reflexiona antes de responder

Varias filas pertenecen a la misma categoría.

¿Debe aparecer una categoría varias veces en el resultado?

Espacio para la solución:

..........................................................................

..........................................................................

---

## Ejercicio 8

### Enunciado

Mostrar todos los clientes excepto aquellos que viven en Santander.

### Pistas

No hace falta utilizar el operador diferencia.

Existe una condición de selección que permite resolver el ejercicio.

Espacio para la solución:

..........................................................................

..........................................................................

---

## Ejercicio 9

### Enunciado

Obtener el nombre de los productos cuyo precio esté comprendido entre ​**50 € y 200 €**​.

Espacio para la solución:

..........................................................................

..........................................................................

---

## Ejercicio 10

### Enunciado

Mostrar únicamente los nombres de los clientes cuyo nombre comience por la letra ​**L**​.

(No es necesario preocuparse todavía por la sintaxis concreta de comparación de cadenas; basta con expresar claramente la condición.)

Espacio para la solución:

..........................................................................

..........................................................................

---

## Ejercicio 11

### Enunciado

Obtener el identificador y el nombre de todos los productos pertenecientes a la categoría **Periféricos** cuyo precio sea inferior a ​**80 €**​.

Espacio para la solución:

..........................................................................

..........................................................................

---

## Ejercicio 12

### Enunciado

La dirección comercial desea elaborar un listado con los nombres de los clientes de Santander.

Explica brevemente por qué resulta más eficiente proyectar únicamente el atributo **Nombre** que devolver la relación completa ​**Cliente**​.

No es necesario escribir una expresión algebraica.

Razona la respuesta utilizando los conceptos estudiados en clase.

Espacio para la respuesta:

..........................................................................

..........................................................................

..........................................................................

..........................................................................

---

## Ejercicio de reflexión

Observa los doce ejercicios anteriores.

Sin escribir ninguna expresión, indica qué operador o combinación de operadores utilizarías en cada uno.

| Ejercicio | Operadores necesarios |
| ----------- | ----------------------- |
| 1         |                       |
| 2         |                       |
| 3         |                       |
| 4         |                       |
| 5         |                       |
| 6         |                       |
| 7         |                       |
| 8         |                       |
| 9         |                       |
| 10        |                       |
| 11        |                       |
| 12        |                       |

Este pequeño análisis permite comprobar si realmente se ha comprendido la función de cada operador antes de avanzar hacia consultas más complejas.

---

## Objetivo alcanzado

Si has podido resolver correctamente la mayoría de estos ejercicios significa que ya dominas los dos operadores más utilizados del Álgebra Relacional.

En el siguiente bloque comenzaremos a trabajar con varias relaciones simultáneamente.

Aparecerán por primera vez el **producto cartesiano** y el ​**JOIN**​, lo que obligará a razonar sobre cómo se relacionan las distintas tablas del modelo.

---

## Ideas clave

* La selección filtra las tuplas que cumplen una condición.
* La proyección conserva únicamente los atributos necesarios.
* Ambos operadores suelen utilizarse conjuntamente.
* Antes de escribir una expresión conviene identificar si el problema requiere filtrar filas, eliminar columnas o ambas cosas.
* Dominar estos operadores simplificará enormemente el estudio de las consultas con varias relaciones.

