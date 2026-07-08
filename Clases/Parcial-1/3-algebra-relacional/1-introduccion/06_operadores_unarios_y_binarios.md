# Operadores unarios y binarios

## Introducción

Una vez comprendido que una relación es un conjunto de tuplas, surge una nueva pregunta.

¿Qué podemos hacer con esas relaciones?

La respuesta constituye el núcleo del Álgebra Relacional.

El Álgebra Relacional define un conjunto de ​**operadores**​, es decir, operaciones matemáticas que reciben una o varias relaciones como entrada y producen siempre una nueva relación como resultado.

Esta última característica es especialmente importante.

Cada operador devuelve otra relación.

Eso significa que el resultado de una operación puede utilizarse inmediatamente como entrada de la siguiente.

Gracias a esta propiedad es posible construir consultas cada vez más complejas combinando operaciones sencillas.

### Una idea heredada de las matemáticas

Cuando estudiamos matemáticas aprendemos que algunos operadores necesitan un único operando y otros necesitan dos.

Por ejemplo:

```text
-8
```

El signo menos actúa únicamente sobre un número.

Se trata de un operador unario.

Sin embargo,

```text
5 + 3
```

requiere dos operandos.

El operador suma es binario.

El Álgebra Relacional sigue exactamente la misma idea.

### Operadores unarios

Los operadores unarios trabajan sobre ​**una única relación**​.

Reciben una relación como entrada y generan otra distinta como resultado.

Los dos operadores unarios más importantes son:

* Selección.
* Proyección.

La **selección** permite conservar únicamente aquellas tuplas que cumplen una determinada condición.

Por ejemplo:

> Clientes cuya ciudad sea Santander.

La ​**proyección**​, por el contrario, mantiene todas las tuplas pero selecciona únicamente determinados atributos.

Por ejemplo:

> Mostrar únicamente el nombre y el correo electrónico de todos los clientes.

En ambos casos solo existe una relación de entrada.

### Operadores binarios

Los operadores binarios necesitan dos relaciones.

A partir de ambas construyen una nueva relación.

Entre los operadores binarios más importantes encontramos:

* Unión.
* Diferencia.
* Intersección.
* Producto cartesiano.
* Diversos tipos de combinación (join), que estudiaremos más adelante.

Supongamos que disponemos de dos relaciones con productos procedentes de distintos almacenes.

Una unión permitiría obtener el conjunto de todos los productos presentes en ambos.

Una diferencia permitiría conocer qué productos aparecen en un almacén pero no en el otro.

Cada operador responde a una necesidad distinta.

### Siempre producen relaciones

Una de las propiedades más elegantes del Álgebra Relacional es su ​**cierre**​.

Esto significa que el resultado de cualquier operador vuelve a ser una relación.

Por ejemplo:

```
Cliente
      ↓
 Selección
      ↓
Nueva relación
      ↓
 Proyección
      ↓
Nueva relación
      ↓
 Unión
      ↓
Nueva relación
```

Esta propiedad permite encadenar operaciones indefinidamente.

De hecho, una consulta SQL aparentemente sencilla suele convertirse internamente en una larga cadena de operadores algebraicos.

### Nuestro caso de estudio

Supongamos que la empresa desea conocer los productos cuyo stock es inferior a diez unidades.

Primero aplicaría una selección sobre la relación ​**Producto**​.

Posteriormente podría proyectar únicamente el nombre del producto y el stock disponible para generar un informe resumido.

Aunque el usuario vea una única consulta, internamente el sistema está combinando varios operadores algebraicos consecutivos.

### Un anticipo de los próximos capítulos

En esta clase únicamente aprenderemos a distinguir entre operadores unarios y binarios.

En las siguientes clases del curso estudiaremos con detalle cada uno de ellos.

Veremos:

* cómo funcionan;
* qué restricciones tienen;
* cuándo pueden combinarse;
* cómo se traducen posteriormente a SQL;
* cómo los utilizan los optimizadores de consultas.

Comprender esta clasificación facilitará enormemente ese aprendizaje.

### Errores frecuentes

Uno de los errores más habituales consiste en pensar que todos los operadores funcionan igual.

En realidad, algunos modifican únicamente las filas, otros únicamente las columnas y otros combinan varias relaciones diferentes.

También es frecuente olvidar que todas las operaciones generan una nueva relación sin modificar las originales.

Esta característica diferencia al Álgebra Relacional de muchos procedimientos imperativos.

### Ideas clave

* Los operadores son las herramientas fundamentales del Álgebra Relacional.
* Los operadores unarios trabajan sobre una única relación.
* Los operadores binarios necesitan dos relaciones como entrada.
* Todas las operaciones producen siempre una nueva relación.
* Esta propiedad permite construir consultas complejas combinando operaciones sencillas de forma progresiva.

