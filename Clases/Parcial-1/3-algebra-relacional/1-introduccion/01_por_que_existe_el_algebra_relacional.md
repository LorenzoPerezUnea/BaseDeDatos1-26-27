# ¿Por qué existe el Álgebra Relacional?

Durante las clases anteriores hemos dedicado un gran esfuerzo a construir una base de datos correctamente diseñada. Hemos identificado entidades, atributos, claves y relaciones hasta obtener un modelo relacional coherente para nuestra empresa de venta de productos tecnológicos.

Sin embargo, una base de datos perfectamente diseñada tiene poco valor si no somos capaces de extraer información de ella.

Imaginemos que el director comercial formula una pregunta aparentemente sencilla:

> ¿Qué clientes han realizado compras superiores a 1.000 euros durante este año?

O que el responsable de almacén necesita saber:

> ¿Qué productos tienen menos de cinco unidades disponibles?

Responder a estas preguntas exige algo más que almacenar datos. Es necesario disponer de un mecanismo que permita expresar consultas de forma precisa y obtener exactamente la información deseada.

### El problema antes de las bases de datos relacionales

En las primeras bases de datos cada fabricante utilizaba su propio sistema de consulta.

Cada producto tenía un lenguaje distinto.

Cada aplicación debía aprender una sintaxis diferente.

No existía una teoría común.

Tampoco existía una forma de demostrar que una consulta era correcta.

Esto hacía muy difícil compartir conocimientos, desarrollar nuevos sistemas o mejorar el rendimiento de las consultas.

Era evidente que hacía falta un modelo matemático independiente de cualquier fabricante.

### La propuesta de Edgar F. Codd

En 1970, Edgar F. Codd presentó el modelo relacional.

Pero ese modelo no solo describía cómo almacenar los datos.

También debía explicar cómo trabajar con ellos.

Para resolver este problema propuso un conjunto de operaciones matemáticas capaces de transformar relaciones en nuevas relaciones.

A ese conjunto de operaciones lo denominó **Álgebra Relacional**.

Su idea era extraordinariamente elegante.

En lugar de diseñar un lenguaje ligado a una implementación concreta, definió una teoría matemática sobre la que cualquier sistema gestor podría construir posteriormente su propio lenguaje de consulta.

### Un lenguaje para pensar

Es importante comprender que el Álgebra Relacional no fue concebida para que los usuarios escribieran consultas diariamente.

Su objetivo principal era proporcionar un lenguaje formal para describir operaciones sobre relaciones.

Gracias a ello fue posible estudiar propiedades como:

- equivalencia entre consultas;
- simplificación de expresiones;
- optimización automática;
- corrección matemática;
- independencia respecto a la implementación física.

Estas propiedades siguen siendo esenciales en los motores modernos de bases de datos.

### Nuestro caso de estudio

En nuestra empresa almacenamos miles de clientes, pedidos, productos y facturas.

Cuando preguntamos:

> «Mostrar todos los productos pertenecientes a la categoría Monitores.»

No estamos pensando todavía en SQL.

Estamos describiendo una operación lógica sobre una relación.

Precisamente eso es lo que formaliza el Álgebra Relacional.

Más adelante aprenderemos que SQL no hace sino ofrecer una sintaxis amigable para expresar estas mismas operaciones.

### Ideas clave

- El Álgebra Relacional nació para proporcionar una base matemática a las consultas sobre bases de datos.
- Su objetivo era ser independiente de cualquier fabricante.
- Permite razonar formalmente sobre las consultas.
- Constituye el fundamento teórico de SQL y de los motores relacionales actuales.
- Comprender el Álgebra Relacional ayuda a entender cómo piensa un SGBD antes incluso de escribir una consulta SQL.

