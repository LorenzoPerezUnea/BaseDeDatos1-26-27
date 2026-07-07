# Validación del modelo

Construir un diagrama Entidad-Relación no significa que el trabajo haya terminado.

De hecho, uno de los errores más frecuentes entre los desarrolladores principiantes consiste en asumir que el primer modelo dibujado es automáticamente correcto.

En los proyectos profesionales ocurre justamente lo contrario.

Una vez finalizado el primer borrador comienza una de las fases más importantes del diseño: ​**la validación del modelo**​.

Validar significa comprobar que el diagrama representa fielmente el funcionamiento del negocio y que puede utilizarse como base para desarrollar la base de datos.

### ¿Por qué validar?

Incluso un modelo aparentemente correcto puede contener errores difíciles de detectar a simple vista.

Por ejemplo:

* Una entidad innecesaria.
* Un atributo olvidado.
* Una cardinalidad incorrecta.
* Una regla de negocio mal interpretada.
* Una relación que no refleja la realidad.

Si estos errores llegan a la implementación, corregirlos será mucho más costoso.

### ¿Quién debe validar?

La validación no corresponde únicamente al diseñador.

Normalmente participan varias personas.

| Participante    | Función                               |
| ----------------- | ---------------------------------------- |
| Analista        | Revisa la coherencia del modelo.       |
| Cliente         | Comprueba que representa el negocio.   |
| Usuarios        | Detectan situaciones reales olvidadas. |
| Equipo técnico | Evalúa la viabilidad del diseño.     |

Cada uno observa el modelo desde una perspectiva distinta.

### Técnicas de validación

Existen numerosas formas de revisar un modelo.

Las más habituales son:

* Leer todas las relaciones en lenguaje natural.
* Revisar las cardinalidades.
* Analizar casos reales del negocio.
* Simular operaciones habituales.
* Comprobar que todas las reglas de negocio están representadas.

No basta con mirar el diagrama.

Hay que ponerlo a prueba.

### Simulación de escenarios

Una técnica especialmente útil consiste en imaginar situaciones reales.

Por ejemplo:

> Un cliente realiza tres pedidos.

¿El modelo lo permite?

> Un producto cambia de categoría.

¿Puede representarse?

> Un empleado abandona la empresa.

¿Qué ocurre con los pedidos que gestionó?

Responder estas preguntas suele revelar errores ocultos.

### Validando nuestro caso de estudio

Tomemos algunas reglas de nuestra empresa comercial.

* Todo pedido pertenece a un cliente.
* Un cliente puede no tener pedidos.
* Un producto pertenece a una categoría.
* Un pedido contiene varios productos.

Ahora intentemos encontrar alguna situación que contradiga estas reglas.

Si no encontramos inconsistencias, el modelo habrá superado esta primera revisión.

### Validación continua

No debemos pensar que la validación ocurre una única vez.

Cada vez que el modelo cambie será necesario repetir el proceso.

Esta práctica evita que una modificación aparentemente pequeña provoque errores en otras partes del sistema.

### Ideas clave

* Todo modelo debe validarse antes de implementarse.
* La validación implica comprobar tanto la estructura como las reglas del negocio.
* Deben participar tanto expertos técnicos como usuarios del negocio.
* Simular situaciones reales ayuda a descubrir errores.
* La validación debe repetirse cada vez que el modelo evoluciona.

