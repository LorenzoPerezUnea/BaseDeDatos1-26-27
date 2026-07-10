# Tipos de datos

## Introducción

Una vez creada la base de datos, el siguiente paso consiste en definir las tablas que almacenarán la información del sistema. Sin embargo, antes de crear una sola columna debemos responder una pregunta fundamental:

**¿Qué tipo de información almacenará cada atributo?**

No todos los datos son iguales.

Un identificador numérico no debe almacenarse igual que un nombre.

Una fecha no debe tratarse como una cadena de texto.

Un precio no debería almacenarse utilizando un número en coma flotante.

Elegir correctamente el tipo de dato es una de las decisiones más importantes durante el diseño físico de una base de datos. Una mala elección puede provocar pérdida de precisión, desperdicio de espacio, disminución del rendimiento o incluso errores en la aplicación.

En este capítulo conoceremos los tipos de datos más utilizados en MySQL y seleccionaremos aquellos que emplearemos durante el resto del curso.

---

### ¿Qué es un tipo de dato?

Un tipo de dato define tres aspectos fundamentales de una columna.

* Qué clase de valores puede almacenar.
* Cuánto espacio ocupará cada valor.
* Qué operaciones podrán realizarse sobre esos datos.

Por ejemplo, una columna destinada a almacenar fechas solo aceptará valores con formato de fecha.

Una columna destinada a almacenar texto aceptará cadenas de caracteres.

Y una columna numérica permitirá realizar operaciones aritméticas.

Gracias a esta información, MySQL puede validar los datos antes de almacenarlos y optimizar la forma en que se guardan en disco.

---

### Tipos numéricos

Los números aparecen constantemente en una base de datos empresarial.

Se utilizan para identificadores, cantidades, precios, porcentajes, existencias y muchos otros valores.

Uno de los tipos más utilizados es:

```sql
INT
```

Permite almacenar números enteros.

Lo utilizaremos para la mayoría de los identificadores del sistema.

Por ejemplo:

```sql
IdCliente INT
```

Otro tipo muy habitual es:

```sql
BIGINT
```

Se utiliza cuando el número de registros puede ser extremadamente elevado.

En nuestro caso práctico no será necesario utilizarlo inicialmente, aunque conviene conocer su existencia.

---

### Números decimales

Un error muy frecuente entre los principiantes consiste en almacenar precios utilizando `FLOAT` o `DOUBLE`.

Por ejemplo:

```sql
Precio FLOAT
```

Aunque aparentemente funciona, esta decisión puede producir pequeños errores de precisión debido a la representación binaria de los números reales.

En aplicaciones empresariales esto resulta inaceptable.

La alternativa recomendada es:

```sql
Precio DECIMAL(10,2)
```

En este caso:

* 10 representa el número máximo de cifras.
* 2 representa las cifras decimales.

Por ejemplo:

| Valor        | Válido |
| -------------- | --------- |
| 12.50        | ✔      |
| 2599.99      | ✔      |
| 125487965.35 | ✔      |
| 12.345       | ✘      |

Durante todo el curso utilizaremos `DECIMAL` para representar precios, importes y cantidades monetarias.

---

### Tipos de texto

La mayoría de las tablas almacenarán información textual.

Por ejemplo:

* nombres;
* direcciones;
* ciudades;
* correos electrónicos;
* teléfonos.

El tipo más utilizado será:

```sql
VARCHAR(n)
```

donde `n` representa el número máximo de caracteres.

Ejemplos:

```sql
Nombre VARCHAR(100)

Ciudad VARCHAR(80)

CorreoElectronico VARCHAR(150)
```

A diferencia de `CHAR`, `VARCHAR` únicamente almacena el espacio necesario para cada valor, por lo que resulta mucho más eficiente cuando la longitud del texto es variable.

Por este motivo utilizaremos `VARCHAR` en prácticamente todas las columnas de texto del proyecto.

---

### Tipos para fechas

Las aplicaciones empresariales registran continuamente información temporal.

Por ejemplo:

* fecha de nacimiento;
* fecha del pedido;
* fecha del pago;
* fecha de envío.

El tipo más sencillo es:

```sql
DATE
```

Ejemplo:

```sql
FechaPedido DATE
```

Almacena únicamente la fecha.

Cuando también resulta necesario registrar la hora utilizaremos:

```sql
DATETIME
```

Más adelante veremos ejemplos prácticos de ambos tipos.

---

### ¿Qué tipos utilizaremos en este curso?

Aunque MySQL dispone de decenas de tipos de datos diferentes, durante las primeras semanas trabajaremos principalmente con los siguientes.

| Tipo     | Uso habitual            |
| ---------- | ------------------------- |
| INT      | Identificadores         |
| VARCHAR  | Texto                   |
| DECIMAL  | Importes económicos    |
| DATE     | Fechas                  |
| DATETIME | Fecha y hora            |
| BOOLEAN  | Valores verdadero/falso |

Esta selección resulta suficiente para construir una base de datos empresarial completa y coincide con los tipos utilizados con mayor frecuencia en proyectos profesionales.

---

### Casos reales

En nuestra empresa comercial utilizaremos estos tipos desde el primer momento.

Por ejemplo:

| Columna           | Tipo          |
| ------------------- | --------------- |
| IdCliente         | INT           |
| Nombre            | VARCHAR(100)  |
| CorreoElectronico | VARCHAR(150)  |
| FechaRegistro     | DATE          |
| LimiteCredito     | DECIMAL(10,2) |

Puede observarse que la elección del tipo depende siempre del significado del dato y no únicamente de su apariencia.

---

### Errores frecuentes

Uno de los errores más habituales consiste en utilizar `VARCHAR` para almacenar números.

Otro error frecuente es emplear `FLOAT` para representar importes monetarios.

También es común definir columnas de texto excesivamente largas "por si acaso", incrementando innecesariamente el espacio ocupado por la base de datos.

### Ideas clave

* Cada columna debe utilizar el tipo de dato más adecuado para la información que almacenará.
* `INT` será el tipo habitual para identificadores.
* `VARCHAR` será el tipo principal para cadenas de texto.
* `DECIMAL` es la opción recomendada para cantidades monetarias.
* `DATE` y `DATETIME` permiten almacenar información temporal de forma eficiente.
* Elegir correctamente los tipos de datos mejora la integridad, el rendimiento y el mantenimiento de la base de datos.

