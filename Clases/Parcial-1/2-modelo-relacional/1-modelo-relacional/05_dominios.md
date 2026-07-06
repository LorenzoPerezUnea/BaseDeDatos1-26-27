# Dominios

Hasta ahora hemos visto que una relación está formada por atributos y que cada atributo almacena información sobre una determinada característica.

Sin embargo, no cualquier valor puede almacenarse en cualquier atributo.

Por ejemplo, tendría poco sentido guardar un número de teléfono en una columna destinada a fechas o escribir el nombre de una ciudad donde debería aparecer un precio.

Para evitar este tipo de errores, el Modelo Relacional introduce el concepto de ​**dominio**​.

### ¿Qué es un dominio?

Un dominio es el **conjunto de valores permitidos** para un atributo.

Dicho de otra forma, define qué tipo de información puede almacenarse en una determinada columna.

Gracias a los dominios es posible detectar muchos errores antes incluso de guardar los datos.

### Algunos ejemplos

Consideremos la siguiente relación:

| Atributo          | Dominio esperado            |
| ------------------- | ----------------------------- |
| Nombre            | Texto                       |
| FechaNacimiento   | Fecha                       |
| Precio            | Número decimal positivo    |
| Edad              | Número entero              |
| CorreoElectronico | Texto con formato de correo |

Cada atributo acepta únicamente valores compatibles con su dominio.

### Más allá del tipo de dato

En muchos casos un dominio es más específico que un simple tipo de dato.

Por ejemplo, un atributo denominado **Nota** podría ser un número entero.

Sin embargo, no cualquier entero sería válido.

El dominio podría establecer que únicamente se permiten valores entre 0 y 10.

De igual forma, un atributo **EstadoPedido** podría admitir únicamente los valores:

* Pendiente
* En preparación
* Enviado
* Entregado

Aunque todos sean textos, el dominio restringe cuáles son aceptables.

### ¿Por qué son importantes?

Los dominios ayudan a mantener la calidad de los datos.

Gracias a ellos:

* Se reducen errores de introducción.
* Los datos son más consistentes.
* Las consultas producen resultados más fiables.
* La base de datos refleja mejor las reglas del negocio.

En los SGBD modernos, estas restricciones se implementan mediante tipos de datos, restricciones (`CHECK`), enumeraciones, claves foráneas y otros mecanismos que estudiaremos más adelante.

### Caso práctico

En la base de datos de nuestra empresa comercial, el atributo **PrecioVenta** nunca debería contener valores negativos.

Del mismo modo, el atributo **CantidadEnStock** debería admitir únicamente números enteros iguales o superiores a cero.

Definir correctamente estos dominios evitará numerosos errores en el futuro.

### Ideas clave

* Un dominio define el conjunto de valores permitidos para un atributo.
* No todos los valores son válidos para todas las columnas.
* Los dominios contribuyen a mantener la coherencia de la información.
* Un dominio puede imponer restricciones adicionales además del tipo de dato.
* Diseñar correctamente los dominios es uno de los primeros pasos para construir bases de datos fiables.

