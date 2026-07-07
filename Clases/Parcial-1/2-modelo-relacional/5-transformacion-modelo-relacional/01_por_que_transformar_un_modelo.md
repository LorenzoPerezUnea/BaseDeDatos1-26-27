# ¿Por qué transformar un modelo?

Durante las seis primeras clases del curso hemos trabajado exclusivamente con el Modelo Entidad-Relación. Gracias a él hemos podido comprender el negocio sin preocuparnos todavía por aspectos técnicos.

Sin embargo, ha llegado el momento de responder una pregunta muy importante:

> **¿Por qué no utilizar directamente el diagrama ER como base de datos?**

La respuesta es sencilla.

Porque un diagrama conceptual describe la realidad, pero no especifica cómo almacenarla dentro de un ordenador.

Para que un sistema gestor como MySQL pueda trabajar con nuestros datos necesitamos convertir ese modelo conceptual en una estructura lógica formada por tablas, columnas y restricciones.

### Dos niveles diferentes

Una buena forma de entender esta transformación consiste en pensar en un arquitecto.

Antes de construir un edificio se realizan planos.

Los planos describen el edificio, pero nadie puede vivir dentro de ellos.

Después llega la fase de construcción.

Con las bases de datos ocurre exactamente lo mismo.

```text
Modelo ER

↓

Modelo Relacional

↓

Base de datos física
```

Cada etapa utiliza el trabajo realizado en la anterior.

### El Modelo ER responde al "qué"

El Modelo Entidad-Relación intenta responder preguntas como:

* ¿Qué objetos existen?
* ¿Cómo se relacionan?
* ¿Qué reglas siguen?
* ¿Qué información debe almacenarse?

No se preocupa todavía por aspectos técnicos.

Su lenguaje está orientado al negocio.

### El Modelo Relacional responde al "cómo"

Una vez comprendido el negocio debemos responder otras preguntas.

* ¿Qué tablas existirán?
* ¿Qué columnas tendrá cada tabla?
* ¿Cuál será la clave primaria?
* ¿Dónde se almacenarán las claves foráneas?
* ¿Cómo representaremos una relación muchos a muchos?

Estas cuestiones pertenecen al Modelo Relacional.

### Mantener el significado

Durante la transformación no debemos perder información.

Todo lo que expresaba el diagrama ER debe seguir estando presente.

Por ejemplo:

| Modelo ER     | Modelo Relacional                 |
| --------------- | ----------------------------------- |
| Entidad       | Tabla                             |
| Atributo      | Columna                           |
| Identificador | Clave primaria                    |
| Relación     | Clave foránea o tabla intermedia |
| Cardinalidad  | Restricciones entre tablas        |

El lenguaje cambia.

El significado permanece.

### Nuestro caso de estudio

Hasta este momento nuestra empresa comercial estaba representada mediante entidades como:

* Cliente
* Producto
* Pedido
* Categoría
* Empleado
* Proveedor

En esta clase aprenderemos a convertir cada una de ellas en tablas reales listas para implementarse en MySQL.

### Ideas clave

* El Modelo ER es conceptual; el Modelo Relacional es lógico.
* Los SGBD trabajan con tablas, no con entidades.
* Transformar un modelo significa cambiar su representación, no su significado.
* Cada elemento del Modelo ER posee una regla de transformación específica.
* El objetivo final es obtener un modelo listo para implementarse mediante SQL.

