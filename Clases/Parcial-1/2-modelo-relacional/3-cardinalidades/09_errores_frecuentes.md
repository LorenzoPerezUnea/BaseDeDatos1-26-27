# Errores frecuentes

Aprender la notación del Modelo Entidad-Relación es relativamente sencillo. Lo realmente difícil es construir un modelo que represente correctamente el funcionamiento de una organización.

Los errores de diseño rara vez producen un fallo inmediato. En muchos casos la base de datos funciona aparentemente bien durante meses, hasta que aparecen nuevos requisitos o aumenta el volumen de información.

Por este motivo es importante conocer los errores más habituales antes de comenzar a diseñar sistemas reales.

### Confundir entidades con atributos

Es uno de los errores más comunes.

Supongamos que queremos modelar clientes.

Algunos estudiantes crean las entidades:

* Cliente
* Nombre
* Teléfono
* Correo

Sin embargo, ​**Nombre**​, **Teléfono** y **Correo** no existen de forma independiente.

Son características del cliente.

Por tanto, deben representarse como atributos.

### Crear entidades innecesarias

El problema contrario también es frecuente.

Por ejemplo, crear una entidad llamada **DirecciónPostal** cuando únicamente contiene:

* Calle
* Número
* Código postal

Si esa dirección pertenece exclusivamente a un cliente y no posee comportamiento propio, probablemente baste con representarla mediante atributos.

Solo cuando una dirección pueda reutilizarse o tenga entidad propia dentro del negocio será conveniente convertirla en una entidad independiente.

### Elegir identificadores inadecuados

Muchos principiantes utilizan como identificador datos que pueden cambiar con el tiempo.

Por ejemplo:

* Nombre.
* Correo electrónico.
* Número de teléfono.

Todos ellos pueden modificarse.

Es preferible utilizar identificadores estables, como ​**IdCliente**​, que permanezcan invariables durante toda la vida del registro.

### Cardinalidades incorrectas

Otro error muy habitual consiste en invertir la cardinalidad.

Por ejemplo:

❌ Un pedido pertenece a muchos clientes.

✔ Un cliente realiza muchos pedidos.

La mejor forma de evitar este error consiste en formular la relación en ambos sentidos y comprobar cuál refleja correctamente el funcionamiento del negocio.

### Ignorar las reglas del negocio

A veces el modelo parece correcto desde un punto de vista técnico, pero no respeta la realidad de la empresa.

Por ejemplo:

* Permitir pedidos sin productos.
* Permitir facturas sin pedido.
* Permitir productos sin categoría cuando el negocio no lo admite.

El modelo debe representar el negocio, no únicamente los datos.

### Pensar demasiado pronto en SQL

Otro error frecuente consiste en diseñar el modelo pensando ya en cómo se implementará.

Durante esta fase todavía no debemos preocuparnos por:

* Tipos de datos.
* Índices.
* Consultas.
* Rendimiento.

Nuestro objetivo consiste únicamente en representar correctamente la realidad del negocio.

### Caso práctico

Si diseñáramos incorrectamente nuestra empresa comercial podrían aparecer problemas como:

* Productos repetidos.
* Pedidos sin cliente.
* Facturas imposibles de relacionar.
* Categorías duplicadas.
* Proveedores inconsistentes.

Corregir estos errores después de que la base de datos esté en producción resultaría mucho más costoso que detectarlos durante el modelado.

### Ideas clave

* La mayoría de errores aparecen durante el análisis, no durante la programación.
* Confundir entidades y atributos produce modelos innecesariamente complejos.
* Los identificadores deben ser estables.
* Las cardinalidades deben reflejar fielmente el negocio.
* Un buen diseño evita problemas durante todo el ciclo de vida de la aplicación.

