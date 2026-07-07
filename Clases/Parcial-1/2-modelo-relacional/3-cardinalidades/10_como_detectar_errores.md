# Cómo detectar errores

Diseñar un diagrama Entidad-Relación no significa que el trabajo haya terminado.

Antes de dar un modelo por válido conviene revisarlo cuidadosamente.

En los proyectos profesionales es habitual realizar varias revisiones, tanto por parte del propio analista como por otros miembros del equipo o incluso por representantes del cliente.

Detectar un error en esta fase resulta mucho más sencillo que corregirlo cuando la base de datos ya contiene miles de registros.

### Revisar cada entidad

El primer paso consiste en analizar cada entidad de forma individual.

Podemos formular preguntas como:

* ¿Representa realmente un objeto del negocio?
* ¿Tiene sentido por sí sola?
* ¿Posee un identificador adecuado?
* ¿Existen entidades duplicadas?

Si alguna respuesta genera dudas, probablemente debamos revisar el diseño.

### Revisar los atributos

Cada atributo también debe analizarse.

Preguntas útiles son:

* ¿Describe realmente a la entidad?
* ¿Está almacenando varios datos en uno solo?
* ¿Puede calcularse a partir de otros?
* ¿Su nombre es suficientemente claro?

Esta revisión ayuda a mantener un modelo limpio y coherente.

### Revisar las relaciones

Una buena práctica consiste en leer las relaciones como si fueran frases en lenguaje natural.

Por ejemplo:

> Un cliente realiza pedidos.

> Un pedido contiene productos.

Si alguna frase resulta extraña o ambigua, probablemente exista un problema de diseño.

### Revisar las cardinalidades

Las cardinalidades deben responder correctamente a preguntas como:

* ¿Puede un cliente realizar varios pedidos?
* ¿Puede un pedido pertenecer a dos clientes?
* ¿Puede un producto aparecer en varios pedidos?

Responder utilizando ejemplos reales del negocio suele facilitar mucho esta comprobación.

### Validar con el cliente

El mejor diagrama posible carece de valor si no representa correctamente el funcionamiento de la empresa.

Por ello, una vez construido el modelo, debe presentarse al cliente para comprobar que refleja fielmente sus procesos.

Durante esta revisión suelen descubrirse nuevas reglas de negocio que obligan a modificar el modelo.

Esto forma parte del proceso normal de desarrollo.

### Una lista de comprobación

Antes de considerar finalizado un modelo conceptual conviene verificar:

* Todas las entidades tienen sentido.
* Todas poseen un identificador.
* Las relaciones representan el negocio.
* Las cardinalidades son correctas.
* No existen datos duplicados.
* Las reglas de negocio están reflejadas.
* El cliente comprende y acepta el modelo.

Esta sencilla revisión evita una gran cantidad de errores posteriores.

### Caso práctico

Antes de transformar el modelo de nuestra empresa comercial al Modelo Relacional realizaremos precisamente esta revisión.

Solo cuando estemos seguros de que el diagrama representa correctamente el negocio comenzaremos la implementación en MySQL.

### Ideas clave

* Todo modelo debe revisarse antes de implementarse.
* Leer las relaciones como frases facilita detectar errores.
* El cliente debe validar el modelo.
* Las revisiones reducen significativamente los costes de desarrollo.
* Un buen modelo es el resultado de varias iteraciones, no del primer borrador.

