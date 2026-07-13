# ¿Qué es DML?

## Introducción

Una base de datos puede compararse con un edificio.

Las clases anteriores estuvieron dedicadas a construir la estructura: levantar los cimientos, crear las habitaciones y definir las conexiones entre ellas.

Ahora que el edificio existe, debemos comenzar a utilizarlo.

En términos de bases de datos, esto significa almacenar información.

El conjunto de instrucciones encargado de insertar, modificar y eliminar registros recibe el nombre de ​**Lenguaje de Manipulación de Datos**​, o ​**Data Manipulation Language (DML)**​.

Si el DDL define la estructura de una base de datos, el DML trabaja sobre el contenido de esa estructura.

---

### El papel del DML

Las operaciones DML actúan directamente sobre las filas de las tablas.

No modifican la estructura de la base de datos.

En su lugar:

* crean nuevos registros;
* modifican registros existentes;
* eliminan registros.

Por ello constituyen el conjunto de instrucciones SQL más utilizado por las aplicaciones.

Cada vez que utilizamos una tienda en línea, una red social o una aplicación bancaria, cientos de instrucciones DML se ejecutan continuamente.

---

### Las principales instrucciones DML

Durante esta clase estudiaremos cuatro operaciones fundamentales.

| Instrucción | Función                        |
| -------------- | --------------------------------- |
| INSERT       | Añade nuevos registros.        |
| UPDATE       | Modifica registros existentes.  |
| DELETE       | Elimina registros.              |
| TRUNCATE     | Vacía completamente una tabla. |

Cada una de ellas responde a una necesidad diferente y presenta ventajas, limitaciones y riesgos que estudiaremos detalladamente.

---

### DDL frente a DML

Es importante no confundir ambos sublenguajes.

| DDL                      | DML                        |
| -------------------------- | ---------------------------- |
| Crea tablas              | Inserta registros          |
| Modifica estructuras     | Modifica datos             |
| Elimina tablas           | Elimina registros          |
| Trabaja sobre el esquema | Trabaja sobre el contenido |

Esta diferencia acompañará al estudiante durante todo el resto del curso.

---

### El flujo normal de trabajo

En un proyecto profesional el trabajo suele seguir siempre el mismo orden.

```text
Diseño conceptual

↓

Modelo relacional

↓

DDL

↓

DML

↓

Consultas

↓

Optimización
```

Hasta ahora hemos completado todas las fases anteriores al DML.

Con esta clase comenzamos a poblar la base de datos.

---

### Nuestro caso práctico

Durante las próximas secciones iremos registrando información sobre:

* clientes;
* empleados;
* categorías;
* productos.

En clases posteriores aparecerán pedidos, facturas, pagos, proveedores e inventario.

La información que insertemos hoy será utilizada continuamente en las consultas SQL que estudiaremos durante el resto del semestre.

---

### Errores frecuentes

Uno de los errores más habituales consiste en intentar insertar información en tablas cuya estructura todavía no ha sido creada.

También es frecuente confundir las instrucciones DDL con las operaciones DML.

Comprender claramente esta diferencia facilitará enormemente el aprendizaje de SQL.

### Ideas clave

* DML manipula los datos almacenados en una base de datos.
* No modifica la estructura, únicamente el contenido.
* Las instrucciones principales son `INSERT`, `UPDATE`, `DELETE` y `TRUNCATE`.
* Todas las aplicaciones utilizan continuamente operaciones DML.
* A partir de esta clase comenzaremos a poblar definitivamente nuestro caso práctico.

