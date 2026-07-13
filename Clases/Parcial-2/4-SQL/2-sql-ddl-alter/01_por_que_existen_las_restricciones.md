# ¿Por qué existen las restricciones?

## Introducción

Hasta el momento hemos aprendido a crear bases de datos, definir tablas y especificar el tipo de información que almacenará cada columna. Sin embargo, una base de datos correctamente diseñada debe hacer algo más que guardar información: debe garantizar que esa información sea correcta.

Imaginemos por un momento que el sistema permitiera registrar dos clientes con el mismo identificador, crear un pedido asociado a un cliente inexistente o almacenar un precio negativo para un producto.

Desde el punto de vista técnico, esos datos podrían ocupar perfectamente un espacio en el disco duro. Sin embargo, desde el punto de vista del negocio serían completamente inválidos.

Las **restricciones** (​*constraints*​) existen precisamente para evitar estas situaciones.

Una restricción es una regla que la propia base de datos hace cumplir automáticamente. Gracias a ellas, la responsabilidad de mantener la integridad de la información no recae únicamente sobre el programador, sino también sobre el Sistema Gestor de Bases de Datos.

Esta idea constituye uno de los principios fundamentales del modelo relacional: ​**los datos deben protegerse dentro de la propia base de datos**​.

---

### La integridad de los datos

En cualquier organización, la información constituye uno de sus activos más importantes.

Una empresa puede reconstruir un programa informático, cambiar de servidor o sustituir una aplicación por otra, pero recuperar datos corruptos suele ser una tarea extremadamente difícil.

Por este motivo, los SGBD incorporan mecanismos que impiden almacenar información inconsistente.

Estas reglas reciben el nombre de ​**restricciones de integridad**​.

Podemos entenderlas como un conjunto de normas que todos los registros deben cumplir antes de ser aceptados por el servidor.

Si una operación viola alguna de estas normas, MySQL cancela automáticamente la operación y devuelve un mensaje de error.

---

### ¿Quién debe validar los datos?

Una duda frecuente consiste en preguntarse si la validación debe realizarla la aplicación o la base de datos.

La respuesta profesional es: ​**ambas**​.

La aplicación debe validar los datos para ofrecer una buena experiencia de usuario y detectar errores lo antes posible.

Sin embargo, la base de datos también debe realizar sus propias comprobaciones.

Esto garantiza que, independientemente de la aplicación utilizada (una página web, una aplicación móvil, una API o un script de administración), las mismas reglas se cumplirán siempre.

La base de datos se convierte así en la última línea de defensa frente a datos incorrectos.

---

### Tipos de restricciones

Durante esta clase estudiaremos las restricciones más utilizadas en MySQL.

| Restricción | Función                                  |
| -------------- | ------------------------------------------- |
| PRIMARY KEY  | Identifica de forma única cada registro. |
| FOREIGN KEY  | Garantiza la relación entre tablas.      |
| UNIQUE       | Impide valores repetidos.                 |
| CHECK        | Obliga a cumplir una condición lógica.  |

Además aprenderemos a añadir estas restricciones incluso después de haber creado una tabla utilizando la sentencia `ALTER TABLE`.

---

### Restricciones durante todo el ciclo de vida

Una característica importante de las restricciones es que actúan continuamente.

No solo se aplican cuando insertamos un registro.

También intervienen cuando:

* modificamos información;
* eliminamos registros;
* añadimos nuevas relaciones;
* cambiamos la estructura de una tabla.

Esto significa que la integridad se mantiene durante toda la vida útil de la base de datos.

---

### El caso práctico

Hasta ahora nuestras tablas eran relativamente independientes.

En las próximas sesiones comenzaremos a conectarlas.

Por ejemplo:

* un producto pertenecerá a una categoría;
* un pedido pertenecerá a un cliente;
* una factura estará asociada a un pedido;
* una línea de pedido hará referencia tanto al pedido como al producto.

Estas relaciones solo serán fiables si la base de datos dispone de las restricciones adecuadas.

---

### Errores frecuentes

Un error habitual consiste en confiar únicamente en las validaciones realizadas por la aplicación.

Otro error frecuente es considerar las restricciones como un obstáculo para el desarrollo, cuando en realidad constituyen uno de los mecanismos más importantes para garantizar la calidad de los datos.

### Ideas clave

* Las restricciones protegen la integridad de la información.
* La base de datos también debe validar los datos, además de la aplicación.
* Las restricciones se aplican automáticamente durante toda la vida de la base de datos.
* Una base de datos sin restricciones puede almacenar información inconsistente.
* En esta clase aprenderemos las principales restricciones disponibles en MySQL.

