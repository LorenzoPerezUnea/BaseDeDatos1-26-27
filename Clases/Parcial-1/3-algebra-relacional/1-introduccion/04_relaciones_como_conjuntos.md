# Relaciones como conjuntos

## Introducción

En las clases anteriores hemos utilizado el término **relación** para referirnos a una tabla del modelo relacional.

Esta simplificación resulta muy útil durante las primeras etapas del aprendizaje, ya que facilita la comprensión del diseño de una base de datos. Sin embargo, cuando comenzamos a estudiar el Álgebra Relacional necesitamos adoptar una perspectiva más rigurosa.

Desde el punto de vista matemático, una relación ​**no es simplemente una tabla**​.

Una relación es un ​**conjunto de tuplas**​.

Esta diferencia puede parecer únicamente terminológica, pero tiene profundas consecuencias sobre el comportamiento de las consultas y sobre el funcionamiento interno de los sistemas gestores de bases de datos.

Comprender esta idea será esencial para interpretar correctamente todos los operadores que estudiaremos a continuación.

### Recordando qué es un conjunto

En matemáticas, un conjunto es una colección de elementos que cumple varias propiedades fundamentales.

Entre ellas destacan las siguientes:

* Un elemento pertenece o no pertenece al conjunto.
* El orden de los elementos no tiene importancia.
* Un mismo elemento no puede aparecer repetido.

Por ejemplo, el conjunto:

```text
{2, 4, 6, 8}
```

representa exactamente la misma información que:

```text
{8, 2, 6, 4}
```

El cambio de orden no altera el conjunto.

Del mismo modo,

```text
{2, 4, 4, 6}
```

sigue representando el mismo conjunto que

```text
{2, 4, 6}
```

porque un elemento no puede existir dos veces dentro de un conjunto.

Estas propiedades serán heredadas por el Álgebra Relacional.

### Una relación es un conjunto de filas

Consideremos la relación **Cliente** de nuestra empresa.

| IdCliente | Nombre       | Ciudad    |
| ----------: | -------------- | ----------- |
|         1 | Ana Ruiz     | Santander |
|         2 | Luis Pérez  | Bilbao    |
|         3 | Marta Gómez | Oviedo    |

Cuando observamos esta tabla solemos interpretarla como una lista ordenada de filas.

Sin embargo, el Álgebra Relacional la interpreta de otra manera.

Cada fila constituye un elemento del conjunto.

La relación completa no es más que el conjunto formado por todas esas tuplas.

En consecuencia:

* el orden visual de las filas carece de significado;
* el orden físico de almacenamiento tampoco forma parte del modelo;
* una misma tupla no puede aparecer duplicada.

### ¿Importa el orden?

Esta idea suele sorprender a quienes comienzan a trabajar con bases de datos.

En una hoja de cálculo, el orden suele tener importancia.

En un documento de texto también.

Pero en una relación matemática no.

Si mañana el motor reorganiza físicamente los registros para optimizar el rendimiento, la relación sigue representando exactamente la misma información.

Por este motivo, una consulta SQL solo devolverá resultados ordenados cuando el usuario lo solicite explícitamente mediante una cláusula adecuada.

El orden no forma parte de la definición de una relación.

### ¿Por qué es importante pensar en conjuntos?

Muchos operadores del Álgebra Relacional proceden directamente de la teoría de conjuntos.

Por ejemplo:

* unión;
* diferencia;
* intersección;
* producto cartesiano.

Todos ellos suponen que trabajan sobre conjuntos y, por tanto, heredan sus propiedades.

Comprender esta visión matemática permitirá entender por qué determinadas operaciones eliminan duplicados o producen determinados resultados.

### Nuestro caso de estudio

Imaginemos que la tabla **Producto** contiene tres artículos.

Aunque el gestor almacene físicamente esos registros en un orden distinto después de crear un índice o reorganizar los datos, el contenido lógico de la relación no cambia.

Seguimos teniendo exactamente el mismo conjunto de productos.

Esta separación entre representación lógica y almacenamiento físico constituye uno de los pilares del modelo relacional.

En las próximas secciones veremos que todas las operaciones del Álgebra Relacional trabajan precisamente sobre esa representación lógica.

### Errores frecuentes

Uno de los errores más habituales consiste en asumir que la primera fila de una tabla tiene algún significado especial.

En realidad, salvo que una consulta solicite expresamente un orden concreto, el SGBD puede devolver las filas en cualquier orden.

Otro error frecuente consiste en pensar que una relación admite duplicados de forma natural. Desde el punto de vista del Álgebra Relacional, una relación es un conjunto y, por tanto, no contiene elementos repetidos.

### Ideas clave

* En Álgebra Relacional una relación se interpreta como un conjunto de tuplas.
* El orden de las filas no forma parte del modelo relacional.
* Las relaciones no contienen duplicados desde el punto de vista matemático.
* Muchos operadores del Álgebra Relacional proceden directamente de la teoría de conjuntos.
* Comprender esta idea facilitará el estudio de todos los operadores que veremos a continuación.

