# Tuplas y atributos desde el Álgebra

## Introducción

En las clases dedicadas al modelo relacional hemos utilizado con frecuencia palabras como ​**fila**​, ​**columna**​, **registro** o ​**campo**​. Estos términos son habituales en el lenguaje cotidiano y también aparecen en numerosos sistemas gestores de bases de datos.

Sin embargo, el Álgebra Relacional utiliza una terminología más precisa.

Una fila recibe el nombre de ​**tupla**​.

Una columna recibe el nombre de ​**atributo**​.

Este cambio de vocabulario no es un simple formalismo académico. Refleja una forma distinta de entender la información almacenada y permite describir las operaciones de manera rigurosa desde un punto de vista matemático.

En este capítulo aprenderemos qué representan exactamente las tuplas y los atributos, por qué reciben esos nombres y cómo intervienen en todas las operaciones del Álgebra Relacional.

### De la tabla a la relación

Consideremos nuevamente una parte de la base de datos de nuestra empresa.

| IdCliente | Nombre       | Ciudad    | FechaRegistro |
| ----------: | -------------- | ----------- | --------------- |
|         1 | Ana Ruiz     | Santander | 2023-03-18    |
|         2 | Luis Pérez  | Bilbao    | 2022-11-02    |
|         3 | Marta Gómez | Oviedo    | 2024-01-15    |

Visualmente observamos una tabla.

Sin embargo, desde el punto de vista del Álgebra Relacional, esta estructura puede describirse de una forma mucho más precisa:

* la relación se denomina ​**Cliente**​;
* cada fila es una ​**tupla**​;
* cada columna representa un ​**atributo**​;
* cada atributo posee un dominio de valores posibles.

Esta descripción elimina cualquier dependencia de cómo la información aparece representada en pantalla.

### ¿Qué es una tupla?

Una **tupla** es un conjunto ordenado de valores que describe una única ocurrencia de una entidad.

En nuestro ejemplo, la primera tupla representa a un cliente concreto.

Podría expresarse de forma simplificada como:

```text
(1, "Ana Ruiz", "Santander", 2023-03-18)
```

Cada posición corresponde a uno de los atributos definidos por la relación.

Es importante destacar que una tupla no es simplemente una fila dibujada sobre una tabla.

Es un objeto matemático perfectamente definido.

Cuando el Álgebra Relacional aplica una operación sobre una relación, en realidad está trabajando con conjuntos de tuplas.

### ¿Qué es un atributo?

Un **atributo** representa una propiedad que describe a todas las tuplas de una relación.

Por ejemplo:

* IdCliente identifica de forma única a cada cliente.
* Nombre almacena el nombre completo.
* Ciudad indica la localidad de residencia.
* FechaRegistro refleja el momento en que el cliente comenzó a formar parte de la empresa.

Todos los clientes poseen exactamente esos atributos, aunque cada uno almacene valores diferentes.

Los atributos definen la estructura de la relación.

Las tuplas contienen los datos concretos.

### El dominio de un atributo

Uno de los aspectos más importantes del modelo relacional es que cada atributo pertenece a un ​**dominio**​.

Un dominio puede entenderse como el conjunto de valores válidos para ese atributo.

Por ejemplo:

| Atributo      | Dominio                    |
| --------------- | ---------------------------- |
| IdCliente     | Números enteros positivos |
| Nombre        | Cadenas de texto           |
| Ciudad        | Cadenas de texto           |
| FechaRegistro | Fechas válidas            |

Gracias a esta definición el sistema puede detectar numerosos errores antes incluso de almacenar la información.

No tendría sentido registrar una fecha dentro del atributo Nombre o almacenar un texto donde se espera un valor numérico.

### Tuplas frente a objetos

En programación orientada a objetos solemos trabajar con clases e instancias.

Aunque ambas ideas guardan cierta semejanza, no deben confundirse.

Una tupla no posee métodos, comportamiento ni identidad propia más allá de sus valores.

El Álgebra Relacional trabaja exclusivamente con datos.

Esta simplicidad constituye una de las razones por las que el modelo relacional ha demostrado ser tan robusto durante décadas.

### Nuestro caso de estudio

Supongamos ahora la relación ​**Producto**​.

| IdProducto | Nombre              | Precio | Stock |
| -----------: | --------------------- | -------: | ------: |
|        101 | Monitor 27"         | 249.90 |    18 |
|        102 | Teclado Mecánico   |  89.95 |    42 |
|        103 | Ratón Inalámbrico |  34.50 |    65 |

Cada fila representa una tupla distinta.

Cada columna representa un atributo.

Cuando posteriormente estudiemos operadores como la selección o la proyección veremos que unos trabajan filtrando tuplas mientras que otros seleccionan atributos concretos.

Por tanto, distinguir claramente ambos conceptos resulta imprescindible para comprender el resto del Álgebra Relacional.

### Errores frecuentes

Un error muy común consiste en utilizar indistintamente los términos "fila", "registro" y "tupla" sin comprender que, dentro del Álgebra Relacional, la palabra correcta es ​**tupla**​, ya que posee un significado matemático preciso.

También es frecuente pensar que los atributos almacenan información. En realidad, quienes almacenan los valores son las tuplas; los atributos únicamente describen qué información contiene cada posición de esas tuplas.

### Ideas clave

* Una tupla representa un elemento individual dentro de una relación.
* Un atributo describe una propiedad común a todas las tuplas.
* Cada atributo pertenece a un dominio que limita los valores permitidos.
* Las operaciones del Álgebra Relacional trabajan sobre conjuntos de tuplas y atributos.
* Distinguir claramente ambos conceptos facilitará el aprendizaje de todos los operadores posteriores.

