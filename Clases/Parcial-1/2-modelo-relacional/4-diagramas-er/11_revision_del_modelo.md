# Revisión del modelo

Antes de transformar un modelo conceptual en un Modelo Relacional conviene realizar una última revisión general.

Esta revisión tiene como objetivo responder una pregunta muy sencilla:

> **¿Está realmente preparado el modelo para convertirse en una base de datos?**

No se trata de buscar la perfección absoluta.

Se trata de comprobar que no existen errores evidentes que puedan complicar la implementación posterior.

### Lista de comprobación

Una buena práctica consiste en revisar siempre los mismos aspectos.

#### Entidades

* ¿Representan objetos reales del negocio?
* ¿Existen entidades duplicadas?
* ¿Falta alguna entidad importante?

#### Atributos

* ¿Todos describen correctamente a su entidad?
* ¿Hay atributos redundantes?
* ¿Existen atributos calculables que no deberían almacenarse?

#### Identificadores

* ¿Todas las entidades poseen un identificador?
* ¿Ese identificador permanecerá estable con el tiempo?

#### Relaciones

* ¿Todas representan una necesidad real?
* ¿Las cardinalidades son correctas?
* ¿Existen relaciones innecesarias?

#### Reglas de negocio

* ¿Todas las restricciones del negocio aparecen reflejadas?
* ¿Las participaciones obligatorias están correctamente representadas?

### Una revisión del caso práctico

Si aplicamos esta lista a nuestra empresa comercial obtenemos el siguiente resultado.

| Elemento                  | Estado           |
| --------------------------- | ------------------ |
| Entidades principales     | ✔ Correctas     |
| Atributos básicos        | ✔ Definidos     |
| Relaciones principales    | ✔ Identificadas |
| Cardinalidades            | ✔ Revisadas     |
| Reglas de negocio         | ✔ Documentadas  |
| Refactorizaciones futuras | ✔ Planificadas  |

Aunque el modelo todavía evolucionará, ya dispone de una base suficientemente sólida.

### Preparación para la siguiente etapa

Con esta revisión termina la fase de diseño conceptual.

A partir de la próxima clase comenzaremos una nueva etapa del curso.

Transformaremos nuestras entidades en tablas, nuestros atributos en columnas y nuestras relaciones en claves foráneas.

En otras palabras, comenzaremos a construir una auténtica base de datos relacional.

### Ideas clave

* Revisar un modelo evita errores costosos durante la implementación.
* Una lista de comprobación ayuda a no olvidar ningún aspecto importante.
* El modelo debe estar validado antes de transformarse al Modelo Relacional.
* La revisión constituye el cierre natural de la fase de análisis.
* Un modelo bien revisado facilita enormemente el trabajo de implementación.

