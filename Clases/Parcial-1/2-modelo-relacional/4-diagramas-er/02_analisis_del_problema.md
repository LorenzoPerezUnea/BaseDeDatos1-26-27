# Análisis del problema

Toda base de datos nace para resolver un problema.

Sin embargo, antes de pensar en entidades, atributos o tablas debemos responder una pregunta mucho más importante:

> **¿Qué necesita realmente la organización?**

El análisis del problema es la fase en la que intentamos comprender el funcionamiento del negocio sin preocuparnos todavía por aspectos técnicos.

En otras palabras, todavía no estamos diseñando una base de datos.

Estamos aprendiendo cómo trabaja la empresa.

### Comprender antes de modelar

Uno de los errores más frecuentes consiste en empezar a proponer soluciones demasiado pronto.

Supongamos que un cliente dice:

> "Necesitamos controlar las ventas de nuestros productos."

Esta frase parece sencilla, pero plantea muchas preguntas.

* ¿Quién vende los productos?
* ¿Existen varias tiendas?
* ¿Los clientes deben registrarse?
* ¿Se permiten devoluciones?
* ¿Hay descuentos?
* ¿Cómo se controla el stock?

Cada respuesta modifica el futuro diseño de la base de datos.

### Reuniones con los expertos

En proyectos reales el analista suele reunirse con personas que conocen perfectamente el negocio.

No necesariamente son informáticos.

Pueden ser:

* responsables de ventas;
* personal administrativo;
* encargados de almacén;
* directivos;
* futuros usuarios del sistema.

Su conocimiento resulta mucho más valioso que cualquier documento técnico.

### Formular las preguntas adecuadas

El objetivo del analista no es obtener respuestas rápidas, sino descubrir cómo funciona realmente la organización.

Algunas preguntas habituales son:

* ¿Qué información necesitan consultar cada día?
* ¿Qué documentos utilizan?
* ¿Qué procesos realizan con mayor frecuencia?
* ¿Qué problemas desean resolver?
* ¿Qué información nunca debería perderse?

Estas preguntas suelen revelar entidades y relaciones que inicialmente habían pasado desapercibidas.

### Analizando nuestro caso de estudio

Recordemos la empresa comercial.

Durante las primeras entrevistas obtenemos información como la siguiente:

* La empresa vende productos tecnológicos.
* Los clientes realizan pedidos.
* Cada pedido contiene uno o varios productos.
* Los productos pertenecen a categorías.
* Los proveedores suministran productos.
* Los empleados gestionan los pedidos.

Todavía no estamos dibujando diagramas.

Simplemente estamos recopilando conocimiento.

### Del lenguaje natural al modelo

Una buena práctica consiste en subrayar los sustantivos y verbos del texto proporcionado por el cliente.

Por ejemplo:

> "Los **clientes** realizan **pedidos** que contienen ​**productos**​."

Los sustantivos suelen convertirse en entidades.

Los verbos suelen indicar relaciones.

Este método no es infalible, pero constituye un excelente punto de partida.

### El análisis nunca termina

Incluso cuando la base de datos ya está funcionando seguirán apareciendo nuevos requisitos.

Por ello el análisis debe entenderse como un proceso continuo de aprendizaje.

Cuanto mejor comprendamos el negocio, mejor será nuestro modelo de datos.

### Ideas clave

* El análisis del problema consiste en comprender el negocio antes de diseñar la base de datos.
* Las reuniones con los expertos son fundamentales.
* Formular buenas preguntas es más importante que proponer soluciones rápidas.
* El lenguaje natural proporciona muchas pistas sobre entidades y relaciones.
* Un buen análisis reduce enormemente los errores durante el diseño del modelo.

