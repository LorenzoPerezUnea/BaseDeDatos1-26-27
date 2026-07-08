# Nombres de columnas

Tan importante como elegir buenos nombres para las tablas es nombrar correctamente sus columnas.

Las columnas representan atributos de una entidad y deben expresar claramente el significado de la información almacenada.

Un nombre poco descriptivo puede provocar confusión incluso años después de haber desarrollado la base de datos.

### Un buen nombre debe responder una pregunta

Cuando leemos una columna deberíamos comprender inmediatamente qué representa.

Por ejemplo:

```text
Nombre
```

es mucho más claro que:

```text
Dato1
```

Del mismo modo:

```text
FechaRegistro
```

describe perfectamente su contenido.

### Evitar abreviaturas

Las abreviaturas solo deberían utilizarse cuando sean ampliamente conocidas.

Por ejemplo:

```text
IdCliente
```

es perfectamente aceptable.

Sin embargo:

```text
NmCli
```

resulta difícil de interpretar.

### Mantener un estilo uniforme

Todas las columnas deberían seguir la misma convención de escritura.

Por ejemplo, en este curso utilizaremos:

```text
IdCliente

Nombre

Apellido

CorreoElectronico

FechaRegistro
```

En lugar de mezclar estilos como:

```text
id_cliente

NombreCliente

FECHA

mail
```

La uniformidad facilita la lectura del código SQL.

### Identificadores

Una convención muy utilizada consiste en nombrar las claves primarias mediante el prefijo **Id** seguido del nombre de la entidad.

Por ejemplo:

```text
IdCliente

IdProducto

IdPedido

IdCategoria
```

Gracias a ello resulta muy sencillo identificar las relaciones entre tablas.

### Claves foráneas

Las claves foráneas deberían conservar exactamente el mismo nombre que la clave primaria a la que hacen referencia.

Por ejemplo:

```text
CLIENTE

IdCliente
```

```text
PEDIDO

IdPedido

IdCliente
```

Esto facilita enormemente la comprensión del modelo.

### Evitar información redundante

No es necesario repetir continuamente el nombre de la tabla.

Por ejemplo, dentro de la tabla CLIENTE basta con escribir:

```text
Nombre
```

No hace falta llamarla:

```text
NombreCliente
```

El contexto ya indica que pertenece a la tabla CLIENTE.

### Ideas clave

* Los nombres de las columnas deben ser descriptivos.
* Deben mantenerse las mismas convenciones en toda la base de datos.
* Las claves primarias suelen comenzar por ​**Id**​.
* Las claves foráneas deberían conservar el mismo nombre que las claves primarias correspondientes.
* Un buen nombre mejora la legibilidad y el mantenimiento del código.

