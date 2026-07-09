# Soluciones guiadas

## Introducción

Este documento no pretende ser únicamente una colección de respuestas correctas.

Su objetivo es mostrar **cómo debe razonarse** cada problema.

En una asignatura universitaria de Bases de Datos, obtener el resultado correcto es importante, pero resulta todavía más importante comprender por qué esa solución es correcta y qué razonamiento conduce a ella.

Durante la corrección en clase el profesor utilizará este documento para comentar distintas estrategias, comparar soluciones alternativas y explicar los errores más frecuentes detectados entre los estudiantes.

Se recomienda intentar resolver todos los ejercicios antes de consultar este apartado.

---

## Metodología de corrección

Para cada ejercicio se seguirá el mismo esquema de análisis:

1. Comprensión del enunciado.
2. Relaciones implicadas.
3. Operadores necesarios.
4. Orden lógico de aplicación.
5. Expresión algebraica.
6. Comentarios y errores frecuentes.

Este procedimiento será el mismo que se utilizará posteriormente durante la resolución de ejercicios de SQL.

---

## Criterios de evaluación

Cada ejercicio puede evaluarse utilizando la siguiente rúbrica.

| Criterio                                     | Puntuación orientativa |
| ---------------------------------------------- | ------------------------: |
| Comprensión correcta del enunciado          |                    20 % |
| Identificación de las relaciones implicadas |                    20 % |
| Selección adecuada de operadores            |                    25 % |
| Orden lógico de aplicación                 |                    20 % |
| Expresión algebraica correcta               |                    15 % |

Aunque la expresión final presente pequeños errores de notación, un razonamiento correcto podrá recibir una parte importante de la puntuación.

---

## Errores frecuentes detectados

Durante la resolución de ejercicios suelen aparecer siempre los mismos problemas.

* Confundir selección con proyección.
* Aplicar un JOIN cuando toda la información pertenece a una única relación.
* Olvidar alguna relación intermedia.
* Proyectar atributos demasiado pronto.
* Omitir la condición de unión.
* Utilizar una diferencia cuando realmente se necesita una selección.
* No leer completamente el enunciado antes de comenzar.

Ser consciente de estos errores ayuda a evitarlos en futuros ejercicios.

---

## Recomendaciones antes del examen

Antes de enfrentarte al examen intenta comprobar que eres capaz de resolver cualquier consulta siguiendo siempre este procedimiento.

1. Leer el enunciado completo.
2. Subrayar la información que debe aparecer en el resultado.
3. Identificar las relaciones necesarias.
4. Dibujar mentalmente el recorrido entre ellas.
5. Elegir los operadores.
6. Ordenarlos correctamente.
7. Escribir finalmente la expresión algebraica.

Si este procedimiento llega a convertirse en un hábito, el paso al lenguaje SQL será mucho más sencillo.

---

## Conclusión

El Álgebra Relacional constituye la base teórica sobre la que se construyen prácticamente todos los lenguajes modernos de consulta.

Las próximas clases introducirán SQL, pero el modo de pensar seguirá siendo exactamente el mismo.

El estudiante que domine el razonamiento algebraico aprenderá SQL con mucha mayor facilidad que quien intente memorizar únicamente la sintaxis.

Por este motivo, el tiempo invertido en este taller representa una de las mejores inversiones para el resto de la asignatura.

---

## Ideas clave

* La calidad de una consulta depende tanto del razonamiento como de la expresión final.
* Resolver muchos ejercicios es la mejor forma de consolidar el Álgebra Relacional.
* Los errores suelen repetirse; identificarlos ayuda a evitarlos.
* El método de análisis aprendido en este taller será reutilizado continuamente en SQL.
* Comprender antes de escribir es la estrategia más eficaz para resolver consultas correctamente.

