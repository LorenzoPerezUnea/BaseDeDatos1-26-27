# ¿Qué es un lenguaje de consulta?

## Introducción

Hasta ahora hemos estudiado cómo diseñar una base de datos correctamente. Hemos identificado entidades, atributos, claves primarias, claves foráneas y relaciones hasta construir un modelo capaz de almacenar la información de nuestra empresa de venta de productos tecnológicos.

Sin embargo, almacenar información es únicamente la mitad del problema.

Una base de datos aporta verdadero valor cuando somos capaces de recuperar exactamente la información que necesitamos en el momento adecuado.

Pensemos en algunas situaciones cotidianas dentro de nuestra empresa:

* El departamento comercial quiere conocer los diez clientes con mayor volumen de compras durante el último año.
* El responsable de almacén necesita identificar los productos cuyo stock ha descendido por debajo del mínimo establecido.
* El departamento financiero desea calcular la facturación mensual.
* El equipo de marketing quiere localizar los clientes que no han realizado ninguna compra en los últimos seis meses.

Todas estas preguntas tienen algo en común: ninguna modifica los datos existentes. Lo único que hacen es solicitar información.

Aquí es donde aparecen los lenguajes de consulta.

### ¿Qué entendemos por consulta?

En el contexto de una base de datos, una **consulta** es una petición formal mediante la cual solicitamos determinada información almacenada en el sistema.

No preguntamos directamente a los archivos ni recorremos manualmente las tablas. En su lugar, describimos qué información queremos obtener y dejamos que el sistema determine la mejor forma de encontrarla.

Esta idea representa uno de los mayores avances introducidos por el modelo relacional.

En lugar de programar un recorrido entre registros, formulamos una pregunta.

La base de datos se encarga del resto.

### Un ejemplo cotidiano

Supongamos que deseamos conocer todos los productos cuyo precio sea inferior a 100 euros.

Desde un punto de vista humano, la petición podría expresarse de muchas formas:

* «Muéstrame los productos baratos.»
* «Quiero ver los artículos de menos de cien euros.»
* «Lista los productos cuyo precio sea inferior a 100 €.»

Todas estas frases tienen el mismo significado para una persona, pero resultan ambiguas para un ordenador.

Un sistema informático necesita una representación precisa y sin ambigüedades.

Por este motivo existen los lenguajes de consulta.

Su función consiste en traducir una necesidad de información a una expresión perfectamente definida.

### Un lenguaje especializado

Un lenguaje de consulta no es un lenguaje de programación de propósito general.

No está diseñado para desarrollar videojuegos, aplicaciones móviles o sistemas operativos.

Su objetivo es mucho más concreto:

**expresar operaciones sobre los datos almacenados en una base de datos.**

Esto permite que el lenguaje sea mucho más sencillo de aprender y, al mismo tiempo, extremadamente potente para resolver problemas relacionados con la información.

### Declarar frente a programar

Una de las características más importantes de los lenguajes de consulta modernos es que son ​**declarativos**​.

Esto significa que el usuario describe el resultado que desea obtener, pero no especifica el procedimiento exacto para conseguirlo.

Por ejemplo, cuando preguntamos:

> "Obtén todos los clientes de Santander."

No indicamos:

* qué tabla abrir primero;
* qué índice utilizar;
* qué registros leer;
* en qué orden recorrer el almacenamiento;
* cuánta memoria reservar.

Todas esas decisiones corresponden al sistema gestor de bases de datos.

Nosotros únicamente declaramos el resultado esperado.

Esta separación entre intención y ejecución constituye una de las principales fortalezas del modelo relacional.

### ¿Todos los lenguajes de consulta son iguales?

No.

A lo largo de la historia han existido numerosos lenguajes de consulta.

Algunos eran propietarios de un fabricante concreto.

Otros estaban diseñados para bases de datos jerárquicas o de red.

Con la aparición del modelo relacional surgieron dos grandes enfoques teóricos:

* el Álgebra Relacional;
* el Cálculo Relacional.

Posteriormente apareció SQL, que tomó ideas de ambos modelos y las adaptó a un lenguaje práctico orientado al trabajo diario.

Aunque hoy SQL sea el estándar de facto, comprender la existencia de estos enfoques ayuda a entender por qué SQL posee determinadas características y limitaciones.

### Nuestro caso de estudio

Supongamos que nuestra empresa dispone de las siguientes tablas simplificadas:

* Cliente
* Pedido
* Producto
* Categoria

Un responsable comercial podría formular preguntas como:

* ¿Qué clientes realizaron algún pedido durante este mes?
* ¿Qué productos nunca se han vendido?
* ¿Qué categorías generan mayor facturación?
* ¿Qué clientes han comprado monitores y teclados en un mismo pedido?

Cada una de estas preguntas representa una consulta distinta.

El objetivo del lenguaje de consulta será expresar todas ellas de manera precisa para que el SGBD pueda ejecutarlas correctamente.

### Relación con el Álgebra Relacional

El Álgebra Relacional constituye uno de los primeros lenguajes formales capaces de expresar este tipo de consultas.

Cada operación algebraica transforma una o varias relaciones en una nueva relación.

A partir de estas operaciones básicas pueden construirse consultas de complejidad creciente.

En las próximas secciones comenzaremos precisamente a estudiar esa forma de razonar.

Antes de escribir una sola sentencia SQL aprenderemos a pensar como lo hace el propio sistema gestor.

### Errores frecuentes

Un error habitual consiste en creer que un lenguaje de consulta es simplemente "una sintaxis para hacer SELECT".

En realidad, un lenguaje de consulta define una forma de expresar operaciones sobre los datos y puede poseer una base matemática muy sólida, como ocurre con el Álgebra Relacional.

También es frecuente pensar que una consulta siempre devuelve una lista de registros. En realidad, una consulta devuelve un nuevo conjunto de datos que puede convertirse posteriormente en la entrada de otras operaciones.

### Ideas clave

* Una consulta es una petición formal de información almacenada en una base de datos.
* Un lenguaje de consulta permite expresar esas peticiones de manera precisa y sin ambigüedades.
* Los lenguajes de consulta modernos son principalmente declarativos: indican qué resultado se desea obtener, no cómo conseguirlo.
* El Álgebra Relacional fue uno de los primeros lenguajes formales para consultar bases de datos relacionales.
* SQL heredará muchas de estas ideas y las convertirá en un lenguaje práctico para el trabajo diario.

