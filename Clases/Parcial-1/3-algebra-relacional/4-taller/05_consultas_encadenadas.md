# Consultas encadenadas

## Introducción

Hasta este momento los ejercicios del taller se han centrado en uno o dos operadores principales.

Sin embargo, las consultas utilizadas en proyectos reales rara vez pueden resolverse mediante una única operación.

Lo habitual es que una consulta combine varias selecciones, uno o varios JOIN y una proyección final.

En este bloque comenzaremos a resolver problemas muy similares a los que aparecerán posteriormente en el examen.

El objetivo ya no consiste únicamente en conocer los operadores, sino en aprender a decidir ​**en qué orden deben aplicarse**​.

Para todos los ejercicios se utilizará el dataset principal del taller.

No es necesario obtener el resultado final de las relaciones.

Lo importante es construir correctamente la expresión algebraica y justificar el orden elegido.

---

## Estrategia recomendada

Antes de resolver cualquier ejercicio sigue siempre estos cinco pasos.

1. Identifica qué información solicita el enunciado.
2. Localiza las relaciones donde se encuentra esa información.
3. Decide qué operadores serán necesarios.
4. Establece el orden lógico de aplicación.
5. Escribe la expresión algebraica.

Intentar escribir directamente la expresión completa suele producir más errores que dedicar unos minutos al análisis previo.

---

## Ejercicio 1

### Enunciado

Obtener el nombre de los clientes de Santander que han realizado algún pedido.

### Reflexiona

* ¿Dónde aparece la ciudad?
* ¿Dónde aparece la relación entre clientes y pedidos?
* ¿En qué momento conviene proyectar el nombre?

Espacio para la solución:

..........................................................................

..........................................................................

..........................................................................

---

## Ejercicio 2

### Enunciado

Mostrar el nombre y el precio de todos los productos vendidos durante el pedido ​**1003**​.

Espacio para la solución:

..........................................................................

..........................................................................

..........................................................................

---

## Ejercicio 3

### Enunciado

Obtener el nombre de los clientes que han comprado productos de la categoría ​**Periféricos**​.

### Pistas

Este ejercicio requiere recorrer todo el modelo de datos.

Intenta dibujar primero el camino entre las relaciones.

Espacio para la solución:

..........................................................................

..........................................................................

..........................................................................

---

## Ejercicio 4

### Enunciado

Mostrar los nombres de los productos comprados por clientes que residen en Bilbao.

Espacio para la solución:

..........................................................................

..........................................................................

..........................................................................

---

## Ejercicio 5

### Enunciado

La dirección desea conocer los nombres de los clientes que han realizado pedidos después del día ​**5 de marzo de 2025**​.

Espacio para la solución:

..........................................................................

..........................................................................

..........................................................................

---

## Ejercicio 6

### Enunciado

Obtener el nombre de todos los productos cuyo precio sea superior a **150 €** y que además hayan sido vendidos al menos una vez.

Espacio para la solución:

..........................................................................

..........................................................................

..........................................................................

---

## Ejercicio 7

### Enunciado

Mostrar el nombre de los clientes que han comprado un ​**SSD 1 TB**​.

No utilices el identificador del producto.

Resuelve el problema utilizando el nombre del artículo.

Espacio para la solución:

..........................................................................

..........................................................................

..........................................................................

---

## Ejercicio 8

### Enunciado

Obtener el nombre de los clientes y los productos que aparecen en cada uno de sus pedidos.

El resultado debe contener únicamente:

* Nombre del cliente.
* Nombre del producto.

Espacio para la solución:

..........................................................................

..........................................................................

..........................................................................

---

## Ejercicio 9

### Enunciado

La empresa desea conocer todos los productos vendidos a clientes de Santander cuyo precio sea inferior a ​**100 €**​.

### Consejo

Intenta identificar todas las selecciones antes de comenzar a escribir la expresión.

Espacio para la solución:

..........................................................................

..........................................................................

..........................................................................

---

## Ejercicio 10

### Enunciado

Mostrar el nombre de los clientes que hayan comprado simultáneamente un **Monitor 27"** y un ​**Ratón Inalámbrico**​.

### Reflexiona

Este es el primer ejercicio del taller que requiere combinar operadores de conjuntos con JOIN.

No intentes resolverlo de una sola vez.

Divídelo en varios pasos.

Espacio para la solución:

..........................................................................

..........................................................................

..........................................................................

..........................................................................

---

## Ejercicio 11

### Enunciado

La empresa desea localizar los clientes registrados que todavía no han realizado ningún pedido.

Explica primero el razonamiento.

Después escribe la expresión algebraica.

Espacio para la solución:

..........................................................................

..........................................................................

..........................................................................

..........................................................................

---

## Ejercicio 12

### Enunciado

La dirección comercial desea generar un informe con:

* nombre del cliente;
* nombre del producto;
* cantidad comprada;
* precio del producto.

No debe aparecer ninguna otra información.

Este ejercicio integra prácticamente todos los operadores estudiados hasta el momento.

Espacio para la solución:

..........................................................................

..........................................................................

..........................................................................

..........................................................................

---

## Ejercicio de análisis

Selecciona dos de los ejercicios anteriores y responde a las siguientes preguntas.

* ¿Qué operador utilizaste primero?
* ¿Cuál fue el último?
* ¿Podría modificarse el orden sin alterar el resultado?
* ¿Cambiaría la eficiencia de la consulta?

Debate las respuestas con el resto de la clase.

---

## Preparación para el examen

Si has podido resolver correctamente la mayoría de los ejercicios de este bloque, ya estás preparado para enfrentarte a problemas similares a los del examen.

En los siguientes apartados aumentará ligeramente la dificultad de los enunciados.

Aparecerán consultas con condiciones múltiples, varios recorridos entre relaciones y problemas en los que será necesario elegir entre distintas estrategias de resolución.

---

## Ideas clave

* Las consultas reales suelen combinar varios operadores.
* Antes de escribir una expresión conviene identificar el recorrido de la información.
* Dividir un problema complejo en pasos sencillos facilita enormemente su resolución.
* El orden de aplicación de los operadores puede influir tanto en la claridad como en la eficiencia de la consulta.
* Dominar las consultas encadenadas constituye el paso previo imprescindible para comenzar a trabajar con SQL y afrontar con éxito el examen.

