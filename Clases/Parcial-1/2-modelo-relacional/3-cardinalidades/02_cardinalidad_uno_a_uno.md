# Cardinalidad uno a uno

Cuando dos entidades se relacionan no solo debemos indicar que existe una relación entre ellas.

También debemos especificar ​**cuántas instancias de una entidad pueden asociarse con instancias de la otra**​.

Esta característica recibe el nombre de ​**cardinalidad**​.

La primera cardinalidad que estudiaremos es la relación ​**uno a uno (1:1)**​.

Aunque es la menos frecuente en bases de datos empresariales, resulta muy útil en determinadas situaciones.

### ¿Qué significa uno a uno?

Una relación uno a uno indica que:

* Cada instancia de la primera entidad puede relacionarse con una única instancia de la segunda.
* Cada instancia de la segunda entidad puede relacionarse con una única instancia de la primera.

En otras palabras, ambas entidades se corresponden individualmente.

### Un ejemplo sencillo

Supongamos que una empresa entrega un ordenador portátil a cada empleado.

Además, cada ordenador solo puede estar asignado a un único empleado.

La situación puede representarse así.

```mermaid
erDiagram

EMPLEADO ||--|| PORTATIL : utiliza
```

Cada empleado tiene un portátil.

Cada portátil pertenece a un empleado.

No existen más combinaciones posibles.

### Otro ejemplo

En algunos países cada ciudadano posee un único documento nacional de identidad.

Del mismo modo, cada documento identifica únicamente a un ciudadano.

Esta también sería una relación uno a uno.

### ¿Por qué separar las entidades?

A menudo surge una pregunta razonable:

> Si la relación es uno a uno, ¿por qué no guardar toda la información en una única entidad?

La respuesta depende del contexto.

Algunos motivos habituales son:

* Separar información confidencial.
* Reducir el número de atributos de una entidad.
* Gestionar datos opcionales.
* Permitir futuras ampliaciones del sistema.

Por ejemplo, la información médica de un empleado podría almacenarse en una entidad independiente por motivos de privacidad.

### ¿Es una cardinalidad frecuente?

No.

En la práctica, las relaciones uno a uno son relativamente escasas.

La mayoría de relaciones empresariales son de tipo uno a muchos.

Por ello debemos analizar cuidadosamente si una relación realmente necesita ser uno a uno o si ambas entidades podrían fusionarse.

### Caso práctico

En nuestra empresa comercial no aparece inicialmente ninguna relación estrictamente uno a uno.

Sin embargo, podríamos incorporar una entidad ​**CredencialAcceso**​.

Cada empleado tendría una única credencial y cada credencial pertenecería a un único empleado.

```mermaid
erDiagram

EMPLEADO ||--|| CREDENCIAL : posee
```

Este sería un ejemplo válido de relación uno a uno.

### Errores frecuentes

Uno de los errores más habituales consiste en crear relaciones uno a uno simplemente porque resulta más sencillo.

Antes de hacerlo debemos preguntarnos:

* ¿Las entidades pueden existir por separado?
* ¿Tiene sentido mantenerlas independientes?
* ¿Podrían fusionarse sin perder información?

Si la respuesta es afirmativa, probablemente una única entidad sea suficiente.

### Ideas clave

* La cardinalidad uno a uno relaciona una única instancia de cada entidad.
* Es menos frecuente que otras cardinalidades.
* Puede utilizarse para separar información o facilitar futuras ampliaciones.
* No debe emplearse cuando ambas entidades representan realmente el mismo concepto.
* Un buen análisis del negocio permite decidir cuándo utilizar este tipo de relación.

