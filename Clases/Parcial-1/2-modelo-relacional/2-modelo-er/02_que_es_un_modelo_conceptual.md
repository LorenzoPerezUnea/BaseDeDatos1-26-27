# ¿Qué es un modelo conceptual?

En la clase anterior estudiamos el Modelo Relacional y vimos cómo representa la información mediante relaciones, atributos y claves. Sin embargo, ese modelo todavía está bastante próximo a la implementación.

Antes de decidir qué tablas existirán o qué tipos de datos utilizará cada columna, debemos comprender el problema que queremos resolver.

Aquí es donde entra en juego el ​**modelo conceptual**​.

### Una representación independiente de la tecnología

Un modelo conceptual describe la información desde el punto de vista del negocio, no desde el punto de vista del ordenador.

Su objetivo consiste en responder preguntas como:

* ¿Qué objetos existen?
* ¿Qué información debemos almacenar sobre ellos?
* ¿Cómo se relacionan entre sí?
* ¿Qué reglas debe cumplir el sistema?

Todavía no hablamos de MySQL, SQL o tipos de datos.

Únicamente describimos la realidad que queremos representar.

### Hablar el lenguaje del cliente

Supongamos que una empresa nos contrata para desarrollar su sistema de gestión.

Durante las primeras reuniones nadie hablará de claves foráneas ni de consultas SQL.

En cambio, aparecerán expresiones como:

* Tenemos clientes.
* Vendemos productos.
* Los pedidos contienen varios artículos.
* Cada empleado pertenece a un departamento.
* Un proveedor puede suministrar muchos productos.

Todas estas afirmaciones pertenecen al modelo conceptual.

### Del lenguaje natural al diagrama

Una de las funciones del analista consiste en transformar las conversaciones con el cliente en un modelo que pueda comprender tanto el equipo técnico como la propia empresa.

Por ejemplo:

```text
Un cliente realiza pedidos.

Cada pedido contiene productos.

Los productos pertenecen a una categoría.
```

Estas frases acabarán convirtiéndose en entidades y relaciones dentro de un diagrama ER.

### ¿Por qué no utilizar directamente tablas?

Porque todavía desconocemos muchos detalles.

Durante esta fase es habitual descubrir nuevas reglas de negocio.

Por ejemplo:

* Un cliente puede tener varias direcciones.
* Algunos productos son digitales.
* Existen proveedores internacionales.
* Un pedido puede cancelarse.

Si hubiéramos comenzado implementando tablas desde el primer día, probablemente tendríamos que modificarlas continuamente.

El modelo conceptual nos permite experimentar y corregir el diseño antes de escribir código.

### El Modelo Entidad-Relación

El lenguaje conceptual que utilizaremos durante el curso será el ​**Modelo Entidad-Relación (ER)**​.

Este modelo representa gráficamente:

* Entidades.
* Atributos.
* Relaciones.
* Restricciones básicas.

En los próximos capítulos estudiaremos cada uno de estos elementos por separado.

### Caso práctico

Nuestra empresa comercial todavía no tiene ninguna base de datos.

Durante las reuniones iniciales únicamente sabemos que existen clientes, empleados, productos, proveedores y pedidos.

Nuestro trabajo consistirá en transformar ese conocimiento en un modelo conceptual que sirva de guía para todo el desarrollo posterior.

### Ideas clave

* Un modelo conceptual representa la realidad del negocio sin depender de una tecnología concreta.
* Se construye antes del modelo relacional y de la implementación.
* Su objetivo es comprender el problema antes de programar.
* El Modelo Entidad-Relación es el modelo conceptual más utilizado para diseñar bases de datos.
* Un buen modelo conceptual facilita enormemente el resto del desarrollo del sistema.

