# Primeros ejercicios

## Introducción

La mejor forma de comprobar que se ha comprendido un nuevo concepto consiste en utilizarlo para resolver problemas.

Hasta este momento hemos estudiado los fundamentos del Álgebra Relacional desde un punto de vista conceptual. Hemos visto por qué nació, cómo interpreta las relaciones y cuál es su relación con SQL.

Ahora es el momento de comenzar a razonar como lo haría un sistema gestor de bases de datos.

En esta primera colección de ejercicios no utilizaremos todavía expresiones algebraicas complejas ni consultas SQL.

El objetivo consiste en aprender a identificar qué operación sería la más adecuada para resolver cada problema.

Lo importante no es escribir símbolos.

Lo importante es pensar correctamente.

---

### Ejercicio 1. ¿Filtrar filas o seleccionar columnas?

Disponemos de la siguiente relación simplificada:

| IdProducto | Nombre              | Precio | Stock |
| -----------: | --------------------- | -------: | ------: |
|        101 | Monitor 27"         | 249,90 |    18 |
|        102 | Ratón Inalámbrico |  34,50 |     6 |
|        103 | Teclado Mecánico   |  89,95 |    42 |

El responsable de almacén necesita conocer únicamente los productos cuyo stock sea inferior a diez unidades.

**Pregunta**

¿Qué operación conceptual debemos realizar?

**Pista**

Pregúntate si deseas conservar todas las filas o únicamente algunas de ellas.

---

### Ejercicio 2. ¿Qué información necesita realmente el usuario?

Partiendo de la misma relación, el departamento comercial únicamente necesita elaborar un catálogo con el nombre y el precio de todos los productos.

**Pregunta**

¿Es necesario eliminar alguna tupla?

¿O únicamente deben mostrarse determinados atributos?

---

### Ejercicio 3. Dos operaciones consecutivas

Ahora el responsable comercial solicita lo siguiente:

> Mostrar únicamente el nombre y el precio de los productos cuyo stock sea inferior a diez unidades.

**Pregunta**

¿Qué dos operaciones deberían aplicarse?

¿En qué orden?

Intenta razonar la respuesta antes de pensar en SQL.

---

### Ejercicio 4. Nuestra tabla Cliente

Consideremos ahora la relación:

| IdCliente | Nombre       | Ciudad    | CorreoElectronico                        |
| ----------: | -------------- | ----------- | ------------------------------------------ |
|         1 | Ana Ruiz     | Santander | [ana@email.com](mailto:ana@email.com)       |
|         2 | Luis Pérez  | Bilbao    | [luis@email.com](mailto:luis@email.com)     |
|         3 | Marta Gómez | Santander | [marta@email.com](mailto:marta@email.com)   |
|         4 | Carlos Díaz | Oviedo    | [carlos@email.com](mailto:carlos@email.com) |

El departamento de marketing desea enviar una campaña únicamente a los clientes de Santander.

Además, solo necesita conocer el nombre y el correo electrónico.

**Preguntas**

* ¿Qué operación debe realizarse primero?
* ¿Qué operación debe realizarse después?
* ¿La relación original cambia?

---

### Ejercicio 5. Identificando operadores

Indica qué tipo de operación representa cada una de las siguientes situaciones.

| Situación                                                       | Operación esperada |
| ------------------------------------------------------------------ | --------------------- |
| Mostrar únicamente los clientes de Bilbao                       |                     |
| Mostrar solo el nombre de todos los clientes                     |                     |
| Obtener únicamente los pedidos del mes actual                   |                     |
| Mostrar únicamente el nombre y el precio de todos los productos |                     |
| Localizar los pedidos cuyo importe supera los 1.000 €           |                     |

No es necesario utilizar todavía la notación algebraica.

Basta con identificar correctamente el tipo de operación.

---

### Ejercicio de reflexión

Sin utilizar SQL, explica con tus propias palabras cómo responderías a la siguiente petición:

> "Quiero conocer el nombre de todos los clientes que han realizado algún pedido durante este año."

No intentes escribir código.

Describe únicamente el razonamiento que seguiría el sistema gestor de bases de datos.

Este ejercicio pretende reforzar una idea muy importante:

Antes de aprender un lenguaje debemos aprender a pensar.

El lenguaje cambiará.

La lógica permanecerá.

### Ideas clave

* El Álgebra Relacional debe entenderse antes de memorizar su sintaxis.
* Cada problema puede analizarse identificando primero qué operación representa.
* Muchas consultas se resuelven combinando varias operaciones sencillas.
* Pensar correctamente facilita enormemente el aprendizaje posterior de SQL.
* La comprensión del razonamiento es más importante que la memorización de símbolos.

