# Buenas prácticas de nomenclatura

## Introducción

Escribir código SQL que funcione es importante.

Escribir código SQL que además sea fácil de leer, mantener y ampliar resulta todavía más importante.

En proyectos pequeños, una mala elección de nombres puede parecer un problema menor. Sin embargo, cuando una base de datos contiene cientos de tablas y miles de columnas, una nomenclatura inconsistente convierte el mantenimiento en una tarea extremadamente difícil.

Por este motivo, prácticamente todas las organizaciones definen un conjunto de convenciones de nomenclatura que deben respetarse durante todo el proyecto.

En esta asignatura utilizaremos una única convención desde el primer día y la mantendremos hasta el final del curso.

---

### Un único idioma

Una de las primeras decisiones consiste en elegir el idioma que utilizarán los nombres de las tablas y columnas.

En proyectos internacionales suele utilizarse el inglés.

Sin embargo, dado que nuestro objetivo es aprender el modelo relacional y SQL, durante este curso utilizaremos nombres en español.

Por ejemplo:

```text
Cliente
Producto
Categoria
Pedido
Factura
Empleado
```

Lo importante no es el idioma elegido, sino mantener la misma decisión durante todo el proyecto.

---

### Singular o plural

Otra cuestión muy habitual consiste en decidir si las tablas deben escribirse en singular o en plural.

Ambas opciones son válidas.

Por ejemplo:

| Singular | Plural    |
| ---------- | ----------- |
| Cliente  | Clientes  |
| Producto | Productos |
| Pedido   | Pedidos   |

En esta asignatura utilizaremos ​**el singular**​.

Así, cada fila representa una instancia de la entidad correspondiente.

---

### Identificadores

Todas las claves primarias seguirán la misma convención.

```text
IdCliente
IdProducto
IdCategoria
IdPedido
IdFactura
IdProveedor
```

Esto facilita enormemente la lectura de consultas SQL y la identificación de las relaciones entre tablas.

---

### Nombres descriptivos

Los nombres deben expresar claramente el significado de cada atributo.

Por ejemplo:

Correcto:

```text
CorreoElectronico
FechaRegistro
Precio
FechaContratacion
```

Poco recomendable:

```text
Dato1
CampoA
Texto
Valor
```

Un nombre ligeramente más largo suele ser preferible a uno demasiado ambiguo.

---

### Evitar abreviaturas innecesarias

Las abreviaturas pueden ahorrar algunos caracteres, pero dificultan la comprensión del código.

Por ejemplo:

| Poco recomendable | Recomendado       |
| ------------------- | ------------------- |
| NomCli            | Nombre            |
| CorreoElec        | CorreoElectronico |
| FecAlta           | FechaRegistro     |

El código se escribe una vez, pero se lee muchas veces.

---

### Uso de mayúsculas

Durante este curso utilizaremos el estilo **PascalCase** para tablas y columnas.

Ejemplos:

```text
Cliente
Producto
FechaRegistro
CorreoElectronico
```

Las palabras reservadas de SQL se escribirán siempre en mayúsculas.

```sql
SELECT
FROM
WHERE
CREATE TABLE
PRIMARY KEY
```

Aunque MySQL no obliga a seguir esta convención, mejora considerablemente la legibilidad del código.

---

### Nuestra convención oficial

A partir de esta clase seguiremos las siguientes reglas.

| Elemento         | Convención                        |
| ------------------ | ------------------------------------ |
| Tablas           | Singular                           |
| Idioma           | Español                           |
| Claves primarias | IdEntidad                          |
| Columnas         | PascalCase                         |
| SQL              | Palabras reservadas en mayúsculas |

Mantener estas reglas de forma constante hará que toda la base de datos resulte uniforme y fácil de comprender.

---

### Errores frecuentes

Uno de los errores más habituales consiste en mezclar idiomas dentro del mismo proyecto.

También es frecuente alternar singular y plural sin seguir ningún criterio.

Finalmente, muchos estudiantes cambian la forma de nombrar los identificadores entre unas tablas y otras, dificultando la lectura de consultas complejas.

### Ideas clave

* La nomenclatura forma parte del diseño de una base de datos profesional.
* La coherencia es más importante que la convención elegida.
* Durante este curso utilizaremos nombres en español y tablas en singular.
* Todas las claves primarias seguirán el patrón `IdEntidad`.
* Mantener una convención uniforme simplifica el desarrollo, el mantenimiento y la comprensión del modelo de datos.

