# Relaciones 1 a 1

Después de transformar entidades y atributos, llega el momento de convertir las relaciones.

Comenzaremos por la menos frecuente: la ​**relación uno a uno (1:1)**​.

Aunque aparece con mucha menos frecuencia que las relaciones uno a muchos, conviene conocer su transformación porque ilustra perfectamente el funcionamiento de las claves foráneas.

### Recordando la cardinalidad 1:1

En una relación uno a uno:

* una instancia de la primera entidad se relaciona con una única instancia de la segunda;
* una instancia de la segunda también se relaciona con una única instancia de la primera.

Ejemplo:

```mermaid
erDiagram

PERSONA ||--|| PASAPORTE : posee
```

Cada persona posee un único pasaporte.

Cada pasaporte pertenece a una única persona.

### ¿Cómo se transforma?

En el Modelo Relacional existen varias posibilidades.

La más habitual consiste en colocar una **clave foránea** en una de las tablas.

```text
PERSONA

IdPersona

Nombre

PASAPORTE

IdPasaporte

Numero

IdPersona
```

La columna **IdPersona** conecta ambas tablas.

### ¿En qué tabla se coloca?

No existe una única respuesta.

Dependerá de la participación y del funcionamiento del negocio.

Normalmente la clave foránea se coloca en la entidad cuya existencia depende más claramente de la otra.

En el ejemplo anterior, el pasaporte depende de la persona.

Por ello parece lógico almacenar allí la referencia.

### ¿Y si ambas entidades siempre existen juntas?

En ocasiones dos entidades mantienen una relación tan estrecha que incluso podrían fusionarse.

Por ejemplo:

```text
Empleado

DatosLaborales
```

Si ambas entidades tienen exactamente la misma vida útil, puede ser preferible convertirlas en una única tabla.

Esta decisión depende del análisis del negocio.

### Nuestro caso de estudio

En la empresa comercial apenas utilizaremos relaciones uno a uno.

La mayoría de relaciones reales serán uno a muchos o muchos a muchos.

No obstante, conocer esta transformación permitirá afrontar modelos más complejos en el futuro.

### Ideas clave

* Una relación 1:1 suele implementarse mediante una clave foránea.
* La elección de la tabla depende del negocio.
* Algunas relaciones 1:1 pueden fusionarse en una única tabla.
* Son menos frecuentes que las relaciones 1:N.
* Deben analizarse cuidadosamente antes de implementarse.

