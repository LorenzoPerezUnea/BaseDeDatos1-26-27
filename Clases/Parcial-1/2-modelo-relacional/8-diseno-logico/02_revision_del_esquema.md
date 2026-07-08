# Revisión del esquema

Antes de crear una base de datos es recomendable realizar una revisión completa del esquema.

Este proceso puede parecer innecesario cuando el proyecto es pequeño, pero en sistemas empresariales evita numerosos errores y costosas modificaciones posteriores.

Una vez creada una base de datos y desarrolladas aplicaciones sobre ella, cambiar el diseño resulta mucho más difícil.

Por ello, conviene detectar cualquier problema antes de escribir la primera instrucción SQL.

### ¿Qué debemos revisar?

La revisión debe comprobar tanto aspectos funcionales como técnicos.

Entre las preguntas más importantes se encuentran las siguientes.

* ¿Todas las entidades del negocio están representadas?
* ¿Existe alguna entidad innecesaria?
* ¿Cada atributo pertenece a la entidad correcta?
* ¿Las relaciones reflejan correctamente el funcionamiento del negocio?
* ¿Se han identificado correctamente las claves primarias?
* ¿Las claves foráneas representan todas las relaciones?
* ¿El modelo está normalizado?

Responder afirmativamente a todas estas preguntas proporciona una elevada confianza en la calidad del diseño.

### Revisando nuestro caso práctico

Nuestro modelo contiene las siguientes entidades principales.

```text
CLIENTE

PRODUCTO

CATEGORIA

PEDIDO

LINEA_PEDIDO

EMPLEADO

PROVEEDOR
```

Cada una representa un concepto claramente diferenciado dentro de la empresa.

Además, las relaciones entre ellas reflejan el funcionamiento cotidiano del negocio.

### Comprobación de redundancias

También debemos asegurarnos de que los datos no aparecen duplicados innecesariamente.

Por ejemplo.

```text
CLIENTE

Direccion
```

La dirección pertenece exclusivamente al cliente.

No debería repetirse dentro de la tabla PEDIDO.

Del mismo modo.

```text
PRODUCTO

Precio
```

Debe almacenarse únicamente en la tabla PRODUCTO y no copiarse en otras tablas salvo que exista una razón de negocio claramente justificada.

### Una lista de comprobación

Antes de implementar cualquier modelo conviene completar una revisión similar a la siguiente.

| Comprobación                  | Estado |
| -------------------------------- | -------- |
| Entidades identificadas        | ✓     |
| Relaciones correctas           | ✓     |
| Claves definidas               | ✓     |
| Modelo normalizado             | ✓     |
| Reglas de negocio revisadas    | ✓     |
| Preparado para implementación | ✓     |

Esta sencilla lista reduce considerablemente la aparición de errores durante las siguientes fases del proyecto.

### Ideas clave

* Revisar el esquema evita errores costosos.
* Es preferible corregir un modelo antes que modificar una base de datos ya implementada.
* Deben revisarse entidades, relaciones, claves y dependencias.
* Una lista de comprobación facilita el proceso.
* Un esquema revisado constituye la mejor base para comenzar la implementación en MySQL.

