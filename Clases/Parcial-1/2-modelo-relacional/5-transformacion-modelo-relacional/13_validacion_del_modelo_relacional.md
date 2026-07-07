# Validación del modelo relacional

Después de transformar el Modelo Entidad-Relación en un conjunto de tablas, aún no podemos dar el trabajo por terminado.

Es necesario comprobar que la transformación ha conservado correctamente toda la información del modelo conceptual.

Este proceso recibe el nombre de ​**validación del modelo relacional**​.

Su objetivo es garantizar que el modelo lógico representa fielmente las reglas del negocio y que podrá implementarse sin inconsistencias.

### ¿Qué debemos comprobar?

La validación consiste en revisar sistemáticamente distintos aspectos del modelo.

Las preguntas más importantes son las siguientes.

#### Tablas

* ¿Todas las entidades se han transformado en tablas?
* ¿Existe alguna tabla innecesaria?
* ¿Falta alguna entidad importante?

#### Columnas

* ¿Todos los atributos aparecen representados?
* ¿Se han eliminado correctamente los atributos compuestos y multivaluados?
* ¿Existen columnas duplicadas?

#### Claves primarias

* ¿Cada tabla posee una clave primaria?
* ¿La clave identifica unívocamente cada registro?
* ¿Puede cambiar con el tiempo?

#### Relaciones

* ¿Todas las relaciones se han implementado?
* ¿Las claves foráneas están en la tabla correcta?
* ¿Las relaciones N:M se han convertido en tablas intermedias?

### Comprobación mediante ejemplos

Una buena técnica consiste en simular operaciones reales.

Por ejemplo:

* Registrar un nuevo cliente.
* Crear un pedido.
* Añadir tres productos al pedido.
* Consultar todos los pedidos de un cliente.

Si el modelo permite realizar todas estas operaciones sin contradicciones, es una buena señal de que la transformación ha sido correcta.

### Comparar con el modelo conceptual

También conviene revisar ambos modelos de forma paralela.

| Modelo ER                | Modelo Relacional                  |
| -------------------------- | ------------------------------------ |
| Cliente                  | Tabla CLIENTE                      |
| Pedido                   | Tabla PEDIDO                       |
| Producto                 | Tabla PRODUCTO                     |
| Cliente realiza Pedido   | Clave foránea IdCliente en PEDIDO |
| Pedido contiene Producto | Tabla LINEAPEDIDO                  |

Cada elemento del modelo conceptual debe tener un equivalente en el modelo relacional.

### Antes de implementar

Una vez validado el modelo relacional estaremos preparados para pasar a la siguiente fase del curso.

En las próximas clases comenzaremos a escribir instrucciones SQL para crear estas tablas físicamente en MySQL.

### Ideas clave

* Todo modelo relacional debe validarse antes de implementarse.
* La validación comprueba tablas, columnas, claves y relaciones.
* Los ejemplos reales ayudan a detectar errores de diseño.
* El modelo relacional debe conservar todas las reglas del modelo conceptual.
* Un buen proceso de validación evita problemas durante la implementación.

