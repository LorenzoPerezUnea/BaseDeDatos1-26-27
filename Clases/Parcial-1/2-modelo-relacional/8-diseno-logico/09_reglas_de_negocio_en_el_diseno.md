# Reglas de negocio en el diseño

Hasta ahora hemos diseñado entidades, atributos, claves e índices. Sin embargo, una base de datos profesional debe representar también las **reglas de negocio** de la organización.

Las reglas de negocio son restricciones que describen cómo funciona realmente una empresa.

No dependen del lenguaje SQL ni del sistema gestor utilizado.

Existen porque el negocio las necesita.

### ¿Qué es una regla de negocio?

Una regla de negocio establece una condición que siempre debe cumplirse.

Por ejemplo:

* un pedido debe pertenecer a un cliente existente;
* un producto no puede tener un precio negativo;
* un empleado debe pertenecer a un departamento;
* una categoría puede contener muchos productos.

Estas reglas forman parte del funcionamiento normal de la empresa.

### ¿Por qué deben aparecer en el diseño?

Si las reglas solo existen en la aplicación y no en la base de datos, cualquier otro programa podría introducir información incorrecta.

La base de datos debe convertirse en la última línea de defensa de la integridad de los datos.

Por ello, muchas reglas deben reflejarse directamente en el diseño lógico.

### Ejemplos en nuestro caso práctico

En la empresa comercial podemos identificar reglas como las siguientes.

| Regla                                              | Representación en el diseño |
| ---------------------------------------------------- | ------------------------------- |
| Todo pedido pertenece a un cliente                 | Clave foránea                |
| Todo producto pertenece a una categoría           | Clave foránea                |
| El precio debe ser positivo                        | Restricción sobre la columna |
| El nombre del producto es obligatorio              | Columna obligatoria           |
| No pueden existir dos clientes con el mismo correo | Restricción de unicidad      |

Observemos que algunas reglas se implementan mediante relaciones y otras mediante restricciones sobre las columnas.

### Pensando antes de programar

Un error frecuente consiste en dejar todas las validaciones para la aplicación.

Por ejemplo, confiar en que el programa comprobará siempre que el precio sea mayor que cero.

Si otro programa accede directamente a la base de datos, esa validación podría desaparecer.

Siempre que sea posible, las reglas importantes deben implementarse también en la base de datos.

### Clasificación de las reglas

Podemos agrupar las reglas de negocio en cuatro grandes categorías.

| Tipo       | Ejemplo                                    |
| ------------ | -------------------------------------------- |
| Existencia | Todo pedido debe tener un cliente.         |
| Dominio    | El precio debe ser positivo.               |
| Unicidad   | El correo electrónico no puede repetirse. |
| Relación  | Un producto pertenece a una categoría.    |

Esta clasificación será muy útil cuando empecemos a utilizar restricciones SQL.

### Nuestro objetivo

En las próximas clases aprenderemos a traducir todas estas reglas al lenguaje SQL utilizando:

* claves primarias;
* claves foráneas;
* restricciones `NOT NULL`;
* restricciones `UNIQUE`;
* restricciones `CHECK`;
* valores por defecto (`DEFAULT`).

### Ideas clave

* Las reglas de negocio describen el funcionamiento de la empresa.
* Deben reflejarse en el diseño lógico siempre que sea posible.
* La base de datos también debe validar la información.
* Las reglas pueden referirse a existencia, dominio, unicidad o relaciones.
* Un buen diseño reduce la posibilidad de introducir datos incorrectos.

