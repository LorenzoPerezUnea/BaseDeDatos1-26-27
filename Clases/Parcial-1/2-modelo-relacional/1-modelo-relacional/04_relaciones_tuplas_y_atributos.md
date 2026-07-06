# Relaciones, tuplas y atributos

Cuando comenzamos a trabajar con bases de datos es habitual utilizar términos como ​**tabla**​, **fila** o ​**columna**​. Estos nombres son muy intuitivos y aparecen en prácticamente todos los gestores de bases de datos.

Sin embargo, el Modelo Relacional utiliza una terminología más precisa.

Comprender estos conceptos permitirá interpretar correctamente la bibliografía especializada y entender mejor el funcionamiento interno de un SGBD.

### Relación

En el Modelo Relacional, una **relación** es el conjunto de información que representa un determinado tipo de entidad del mundo real.

En la práctica, una relación suele representarse como una tabla.

Por ejemplo, la información de todos los clientes de una empresa constituye una relación.

| IdCliente | Nombre      | Ciudad    |
| ----------: | ------------- | ----------- |
|         1 | Ana López  | Santander |
|         2 | Carlos Ruiz | Bilbao    |

Aunque visualmente vemos una tabla, conceptualmente estamos trabajando con una relación.

### Tupla

Cada fila de una relación recibe el nombre de ​**tupla**​.

Una tupla representa un único elemento del conjunto.

En nuestro ejemplo:

|   IdCliente | Nombre               | Ciudad              |
| ------------: | ---------------------- | --------------------- |
| **1** | **Ana López** | **Santander** |

Esta fila constituye una tupla porque describe un único cliente.

Cada cliente almacenado dará lugar a una nueva tupla.

### Atributo

Las columnas reciben el nombre de ​**atributos**​.

Cada atributo describe una característica de las tuplas.

En el ejemplo anterior encontramos tres atributos:

* IdCliente
* Nombre
* Ciudad

Todos los clientes poseen exactamente esos mismos atributos, aunque sus valores sean diferentes.

### Una analogía sencilla

Podemos imaginar una ficha de biblioteca.

Cada ficha describe un libro.

* La colección completa de fichas sería la ​**relación**​.
* Cada ficha individual sería una ​**tupla**​.
* Cada dato de la ficha (título, autor, editorial...) sería un ​**atributo**​.

Esta analogía resulta útil para distinguir claramente los tres conceptos.

### Terminología práctica

En el trabajo cotidiano es muy frecuente utilizar ambos vocabularios de forma indistinta.

| Modelo Relacional | Uso habitual    |
| ------------------- | ----------------- |
| Relación         | Tabla           |
| Tupla             | Fila o registro |
| Atributo          | Columna o campo |

Aunque en el lenguaje coloquial se hable de tablas y filas, durante este curso iremos utilizando progresivamente la terminología formal.

### Caso práctico

La relación **Clientes** contendrá una tupla por cada cliente de nuestra empresa.

Cada tupla tendrá atributos como:

* IdCliente
* Nombre
* Apellidos
* Teléfono
* Correo electrónico

Más adelante añadiremos muchas más relaciones, todas ellas conectadas entre sí.

### Ideas clave

* Una relación representa un conjunto de información sobre un mismo tipo de elemento.
* Una tupla representa un único registro de la relación.
* Un atributo describe una característica de cada tupla.
* Tabla, fila y columna son los nombres habituales de relación, tupla y atributo.
* Comprender esta terminología facilitará el estudio del Modelo Relacional.

