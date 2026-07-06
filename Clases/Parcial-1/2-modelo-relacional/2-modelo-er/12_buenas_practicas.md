# Buenas prácticas

Diseñar una base de datos no consiste únicamente en conocer la sintaxis de un diagrama Entidad-Relación.

Dos personas pueden utilizar exactamente la misma notación y, sin embargo, producir modelos con una calidad muy diferente.

La diferencia suele encontrarse en las ​**buenas prácticas de modelado**​.

Estas recomendaciones no son reglas obligatorias, pero ayudan a construir modelos más claros, consistentes y fáciles de mantener.

### Comprender el negocio antes de modelar

La primera buena práctica consiste en escuchar al cliente antes de empezar a dibujar entidades.

Muchas bases de datos mal diseñadas nacen porque el desarrollador intenta imponer una solución antes de comprender realmente el problema.

El modelo debe describir el negocio, no las preferencias del programador.

### Utilizar nombres claros

Los nombres de entidades y atributos deben ser fáciles de entender.

Es preferible utilizar:

* Cliente
* Producto
* Pedido

En lugar de:

* Clt
* Prod
* Tbl001

Un nombre claro reduce la posibilidad de errores y facilita la comunicación dentro del equipo.

### Una entidad, un único concepto

Cada entidad debe representar un único tipo de objeto.

Por ejemplo, una entidad llamada **ClientePedidoProducto** probablemente esté mezclando varias ideas diferentes.

En ese caso conviene dividirla en varias entidades relacionadas.

### Evitar duplicar información

Siempre que sea posible, la información debe almacenarse una sola vez.

Por ejemplo, si el nombre del cliente ya aparece en la entidad ​**Cliente**​, no debería volver a escribirse en la entidad ​**Pedido**​.

Las relaciones permitirán acceder a esa información cuando sea necesario.

Este principio será la base de la normalización que estudiaremos más adelante.

### No añadir atributos innecesarios

Es habitual intentar almacenar todos los datos imaginables "por si acaso".

Sin embargo, cada nuevo atributo incrementa la complejidad del sistema.

Conviene comenzar con los datos realmente necesarios e incorporar nuevos atributos únicamente cuando el negocio lo requiera.

### Revisar el modelo

Un buen modelo nunca se da por terminado tras el primer borrador.

Antes de aprobarlo conviene revisar cuestiones como:

* ¿Todas las entidades tienen sentido?
* ¿Existen atributos duplicados?
* ¿Las relaciones representan correctamente el negocio?
* ¿Los identificadores son adecuados?
* ¿Falta alguna entidad importante?

Esta revisión suele descubrir errores que pasarían desapercibidos durante el diseño inicial.

### Pensar en el futuro

La base de datos debe resolver las necesidades actuales, pero también facilitar futuras ampliaciones.

Por ejemplo, aunque hoy la empresa tenga una única tienda, quizá dentro de unos años abra nuevas sucursales.

Un diseño flexible permitirá incorporar esos cambios sin reconstruir completamente la base de datos.

### Caso práctico

Durante el resto del curso aplicaremos siempre estas recomendaciones.

Cada vez que ampliemos la empresa comercial revisaremos el modelo antes de implementar nuevas tablas en MySQL.

Este hábito nos ayudará a construir una base de datos robusta y preparada para evolucionar.

### Ideas clave

* Comprender el negocio es más importante que empezar a programar rápidamente.
* Los nombres deben ser claros y consistentes.
* Cada entidad debe representar un único concepto.
* Conviene evitar información duplicada y atributos innecesarios.
* Todo modelo debe revisarse antes de convertirse en una base de datos real.

