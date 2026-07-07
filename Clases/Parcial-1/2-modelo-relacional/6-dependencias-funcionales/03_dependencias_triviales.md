# Dependencias triviales

Una vez comprendido el concepto general de dependencia funcional, podemos comenzar a clasificarlas.

La primera categoría recibe el nombre de ​**dependencias triviales**​.

Aunque su nombre pueda hacer pensar que carecen de importancia, son fundamentales para comprender las reglas formales del Modelo Relacional y las Formas Normales.

### ¿Qué significa "trivial"?

Una dependencia funcional es **trivial** cuando el atributo situado a la derecha ya forma parte del conjunto de atributos situado a la izquierda.

En otras palabras, estamos afirmando algo que siempre será cierto.

Por ejemplo:

```text
A → A
```

o bien

```text
(A, B) → A
```

o también

```text
(A, B, C) → B
```

Todas ellas son dependencias triviales.

### ¿Por qué siempre son ciertas?

Pensemos en una frase muy sencilla.

> Si conozco el número de matrícula de un coche, entonces conozco el número de matrícula de ese coche.

Parece una afirmación absurda.

Sin embargo, es completamente correcta.

No aporta información nueva, pero nunca será falsa.

Lo mismo ocurre con las dependencias triviales.

### Ejemplo en nuestro caso de estudio

Supongamos la tabla PRODUCTO.

| IdProducto | Nombre | Precio | Stock |
| ------------ | -------- | -------: | ------: |
| 101        | Ratón |  18.90 |    24 |

Las siguientes dependencias son triviales.

```text
IdProducto → IdProducto
```

```text
(IdProducto, Precio) → Precio
```

```text
(IdProducto, Nombre, Stock) → Nombre
```

En todos los casos, el atributo de la derecha ya estaba presente en la izquierda.

### ¿Para qué sirven?

En el diseño práctico apenas utilizaremos dependencias triviales.

Sin embargo, son muy importantes porque aparecen continuamente en las demostraciones matemáticas relacionadas con la normalización y con los axiomas de Armstrong.

Además, permiten definir formalmente qué entendemos por una dependencia ​**no trivial**​, que será mucho más interesante desde el punto de vista del diseño.

### Cómo reconocerlas

Existe una regla muy sencilla.

> Si todos los atributos situados a la derecha ya aparecen a la izquierda, la dependencia es trivial.

Por ejemplo:

| Dependencia      | ¿Es trivial? |
| ------------------ | --------------- |
| A → A           | Sí           |
| (A, B) → B      | Sí           |
| (A, B) → A      | Sí           |
| (A, B) → (A, B) | Sí           |
| A → B           | No            |

### Ideas clave

* Una dependencia trivial siempre es verdadera.
* El lado derecho está contenido en el lado izquierdo.
* No aporta información nueva sobre el modelo.
* Es importante para la teoría del Modelo Relacional.
* Sirve como base para definir las dependencias no triviales.

