# ¿Por qué existen los modelos de datos?

Podría parecer que basta con almacenar información en una base de datos para resolver cualquier problema. Sin embargo, la forma en que organizamos los datos influye directamente en la facilidad para consultarlos, modificarlos y mantenerlos.

A lo largo de la historia de la informática se han propuesto distintos modelos de datos porque cada uno intenta resolver problemas diferentes.

No existe un modelo universalmente perfecto. Cada uno presenta ventajas e inconvenientes dependiendo del tipo de información que se desea almacenar.

### Los primeros sistemas

Las primeras aplicaciones informáticas almacenaban la información en archivos.

Cada programa organizaba los datos según sus propias necesidades.

Esta estrategia funcionaba mientras las aplicaciones eran pequeñas, pero pronto comenzaron a aparecer problemas:

* Información duplicada.
* Datos inconsistentes.
* Gran dificultad para compartir información.
* Dependencia entre programas y archivos.

Estos inconvenientes impulsaron el desarrollo de modelos de datos más estructurados.

### La evolución de los modelos

Con el paso de los años aparecieron distintos enfoques.

| Modelo              | Características                                                       |
| --------------------- | ------------------------------------------------------------------------ |
| Jerárquico         | Organiza los datos en forma de árbol.                                 |
| En red              | Permite múltiples conexiones entre registros.                         |
| Relacional          | Organiza la información mediante tablas relacionadas.                 |
| Orientado a objetos | Integra conceptos de la programación orientada a objetos.             |
| NoSQL               | Diseñado para grandes volúmenes de datos y necesidades específicas. |

Cada modelo responde a necesidades diferentes.

Durante este curso nos centraremos en el ​**Modelo Relacional**​, ya que constituye la base de la mayoría de aplicaciones empresariales actuales.

### ¿Por qué triunfó el Modelo Relacional?

Antes del Modelo Relacional, muchos sistemas eran difíciles de mantener porque la forma de acceder a los datos dependía de su organización física.

Edgar F. Codd propuso una idea revolucionaria: el usuario debía preocuparse únicamente por ​**qué información necesitaba**​, no por ​**cómo estaba almacenada**​.

Esta separación simplificó enormemente el desarrollo de aplicaciones y convirtió al Modelo Relacional en el estándar dominante durante las décadas siguientes.

### ¿Siguen existiendo otros modelos?

Sí.

Actualmente conviven distintos modelos de bases de datos.

Por ejemplo, una red social puede utilizar bases de datos relacionales para gestionar usuarios y pagos, mientras emplea bases de datos NoSQL para almacenar grandes cantidades de publicaciones o mensajes.

Elegir un modelo adecuado depende siempre del problema que se desea resolver.

### Caso práctico

Nuestra empresa comercial necesita gestionar clientes, productos, pedidos y facturas.

Toda esta información posee una estructura muy bien definida y numerosas relaciones entre los distintos elementos.

Por este motivo, el Modelo Relacional resulta una elección excelente para este proyecto.

### Ideas clave

* Los modelos de datos surgieron para organizar mejor la información.
* Existen distintos modelos porque no todos los problemas son iguales.
* El Modelo Relacional simplificó enormemente el desarrollo de aplicaciones.
* Actualmente conviven modelos relacionales y no relacionales.
* Elegir un modelo adecuado depende del tipo de información que se desea gestionar.

