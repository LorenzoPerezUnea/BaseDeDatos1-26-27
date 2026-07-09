# Ejercicios de unión, intersección y diferencia

## Introducción

Hasta este momento todas las consultas del taller han consistido en filtrar información o combinar varias relaciones mediante JOIN.

Sin embargo, existen problemas que requieren comparar dos conjuntos de datos completos.

Por ejemplo:

* clientes que pertenecen a dos promociones distintas;
* productos disponibles en dos almacenes;
* clientes que han comprado durante dos campañas comerciales;
* artículos que aparecen en un catálogo pero no en otro.

Este tipo de situaciones se resuelven mediante los operadores de teoría de conjuntos.

Aunque aparecen con menor frecuencia que la selección o el JOIN, constituyen herramientas muy útiles y forman parte de los fundamentos del Álgebra Relacional.

En este bloque utilizaremos algunas relaciones auxiliares independientes del dataset principal.

Su único objetivo es facilitar el estudio de estos operadores.

---

## Relaciones auxiliares

### ClientesNewsletter

Clientes suscritos al boletín de noticias.

| IdCliente |
| ----------: |
|         1 |
|         2 |
|         3 |
|         6 |

---

### ClientesPremium

Clientes pertenecientes al programa de fidelización.

| IdCliente |
| ----------: |
|         1 |
|         3 |
|         5 |

---

### ProductosPromocionVerano

| IdProducto |
| -----------: |
|        101 |
|        102 |
|        104 |

---

### ProductosPromocionInvierno

| IdProducto |
| -----------: |
|        103 |
|        104 |
|        105 |

---

## Ejercicio 1

### Enunciado

Obtener todos los clientes que pertenezcan al programa Newsletter **o** al programa Premium.

### Reflexiona

¿Qué palabra del enunciado indica el operador adecuado?

Espacio para la solución:

..........................................................................

..........................................................................

---

## Ejercicio 2

### Enunciado

Obtener únicamente los clientes que pertenezcan simultáneamente al programa Newsletter y al programa Premium.

Espacio para la solución:

..........................................................................

..........................................................................

---

## Ejercicio 3

### Enunciado

Obtener los clientes suscritos al boletín que todavía no pertenecen al programa Premium.

Espacio para la solución:

..........................................................................

..........................................................................

---

## Ejercicio 4

### Enunciado

La empresa desea lanzar una campaña dirigida a todos los productos que aparezcan en cualquiera de las promociones de verano o invierno.

¿Qué operador utilizarías?

Espacio para la solución:

..........................................................................

..........................................................................

---

## Ejercicio 5

### Enunciado

La dirección quiere identificar únicamente los productos que aparecen en ambas promociones.

Espacio para la solución:

..........................................................................

..........................................................................

---

## Ejercicio 6

### Enunciado

Obtener los productos exclusivos de la promoción de verano.

Es decir, aquellos que no aparecen en la promoción de invierno.

Espacio para la solución:

..........................................................................

..........................................................................

---

## Ejercicio 7

### Enunciado

Explica por qué las relaciones utilizadas en una unión deben ser compatibles.

No es necesario escribir una expresión algebraica.

Razona tu respuesta.

Espacio para la respuesta:

..........................................................................

..........................................................................

..........................................................................

..........................................................................

---

## Ejercicio 8

### Enunciado

¿Sería correcto intentar realizar una unión entre las relaciones **Cliente** y ​**Producto**​?

Justifica la respuesta indicando qué condición dejaría de cumplirse.

Espacio para la respuesta:

..........................................................................

..........................................................................

..........................................................................

---

## Ejercicio 9

### Enunciado

Observa las siguientes relaciones.

A = {1,2,3,4}

B = {3,4,5}

Indica el resultado de:

* A ∪ B
* A ∩ B
* A − B
* B − A

No es necesario utilizar ninguna tabla.

Espacio para la solución:

..........................................................................

..........................................................................

---

## Ejercicio 10

### Enunciado

Una empresa dispone de dos almacenes.

Cada almacén mantiene un listado con los identificadores de los productos disponibles.

Explica qué operador utilizarías para responder a las siguientes preguntas.

| Pregunta                                             | Operador |
| ------------------------------------------------------ | ---------- |
| Productos disponibles en cualquiera de los almacenes |          |
| Productos disponibles en ambos almacenes             |          |
| Productos exclusivos del almacén A                  |          |
| Productos exclusivos del almacén B                  |          |

---

## Ejercicio 11

### Enunciado

Indica si las siguientes afirmaciones son verdaderas o falsas y justifica brevemente la respuesta.

| Afirmación                                                             | V/F |
| ------------------------------------------------------------------------- | ----- |
| La unión elimina automáticamente los duplicados.                      |     |
| La diferencia es conmutativa.                                           |     |
| La intersección devuelve únicamente los elementos comunes.            |     |
| El orden de los operandos en una diferencia no influye en el resultado. |     |

Espacio para las respuestas:

..........................................................................

..........................................................................

..........................................................................

---

## Ejercicio 12

### Enunciado

La empresa desea obtener el listado de clientes registrados que todavía no han realizado ningún pedido.

Utiliza las relaciones del dataset principal.

No es necesario escribir la solución completa.

Indica únicamente:

* qué relaciones intervienen;
* qué operador principal utilizarías;
* qué información deberías obtener previamente para poder resolver el ejercicio.

Este problema será muy similar a uno de los que aparecerán posteriormente en el examen.

Espacio para la respuesta:

..........................................................................

..........................................................................

..........................................................................

..........................................................................

---

## Ejercicio de reflexión

Antes de continuar, intenta responder sin consultar los apuntes.

* ¿Qué operador representa la palabra "o"?
* ¿Qué operador representa la palabra "y"?
* ¿Qué operador representa la expresión "pero no"?
* ¿Por qué la diferencia no es conmutativa?
* ¿Qué significa que dos relaciones sean compatibles?

Si estas preguntas pueden responderse con facilidad, ya dominas los operadores fundamentales de teoría de conjuntos aplicados al Álgebra Relacional.

---

## Ideas clave

* La unión reúne los elementos de dos relaciones compatibles.
* La intersección conserva únicamente los elementos comunes.
* La diferencia elimina de una relación los elementos presentes en otra.
* La compatibilidad entre relaciones es un requisito imprescindible para aplicar estos operadores.
* Los operadores de conjuntos permiten resolver problemas frecuentes relacionados con campañas, promociones, inventarios y comparaciones entre colecciones de datos.

