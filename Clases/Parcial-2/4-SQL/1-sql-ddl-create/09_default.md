# DEFAULT

## Introducción

En el capítulo anterior aprendimos a utilizar la restricción `NOT NULL` para obligar a que determinadas columnas contengan siempre un valor.

Sin embargo, existe una situación muy habitual en el desarrollo de aplicaciones.

En ocasiones un dato no es obligatorio porque el propio sistema puede asignarle automáticamente un valor razonable.

Por ejemplo:

* Todo cliente nuevo podría registrarse inicialmente como ​**Activo**​.
* La fecha de creación de un pedido podría ser la fecha actual.
* Un producto recién creado podría comenzar con un stock de cero.
* Un descuento podría ser inicialmente del 0 %.

En todos estos casos el usuario no necesita escribir explícitamente el valor.

La base de datos puede hacerlo automáticamente mediante la restricción ​**DEFAULT**​.

Esta característica simplifica el trabajo del desarrollador, reduce errores y hace que los datos almacenados sean más consistentes.

---

### ¿Qué es un valor por defecto?

Un valor por defecto es el que MySQL asignará automáticamente a una columna cuando el usuario no proporcione ningún valor durante una inserción.

Es importante destacar que ​**DEFAULT no sustituye al usuario**​.

Simplemente proporciona un valor inicial cuando este no se especifica.

Si el usuario introduce un valor diferente, MySQL utilizará el valor indicado.

---

### Añadiendo una columna con DEFAULT

Vamos a ampliar ligeramente nuestra tabla `Cliente`.

Cada cliente tendrá un estado que indicará si su cuenta está activa.

Recrearemos la tabla.

```sql
DROP TABLE IF EXISTS Cliente;

CREATE TABLE Cliente (

    IdCliente INT PRIMARY KEY,

    Nombre VARCHAR(100) NOT NULL,

    CorreoElectronico VARCHAR(150) NOT NULL,

    Ciudad VARCHAR(80),

    FechaRegistro DATE,

    Activo BOOLEAN DEFAULT TRUE

);
```

La nueva columna `Activo` utilizará automáticamente el valor `TRUE` cuando no indiquemos otro diferente.

---

### Comprobando el valor por defecto

Podemos verificar la estructura de la tabla.

```sql
DESC Cliente;
```

La salida mostrará una nueva columna.

| Field  | Default |
| -------- | --------- |
| Activo | 1       |

En MySQL, el valor lógico `TRUE` suele representarse internamente mediante el número ​**1**​.

---

### Insertando registros utilizando DEFAULT

Ahora insertaremos un cliente sin indicar el valor de `Activo`.

```sql
INSERT INTO Cliente
(
    IdCliente,
    Nombre,
    CorreoElectronico,
    Ciudad,
    FechaRegistro
)
VALUES
(
    1,
    'Ana Ruiz',
    'ana@empresa.com',
    'Santander',
    '2026-09-15'
);
```

Observemos que la columna `Activo` no aparece en la lista.

Consultemos el contenido de la tabla.

```sql
SELECT *
FROM Cliente;
```

Obtendremos un resultado similar.

| IdCliente | Nombre   | Activo |
| ----------: | ---------- | -------- |
|         1 | Ana Ruiz | 1      |

Aunque no hemos proporcionado ningún valor, MySQL ha utilizado automáticamente el valor definido mediante `DEFAULT`.

---

### Sobrescribiendo el valor por defecto

El hecho de existir un valor por defecto no significa que estemos obligados a utilizarlo.

También podemos especificar otro valor.

```sql
INSERT INTO Cliente
VALUES
(
    2,
    'Pedro López',
    'pedro@empresa.com',
    'Bilbao',
    '2026-09-20',
    FALSE
);
```

En este caso MySQL almacenará el valor indicado por el usuario.

---

### Otros ejemplos habituales

Durante el resto del curso utilizaremos `DEFAULT` en numerosas ocasiones.

Algunos ejemplos típicos son:

| Columna   | Valor por defecto |
| ----------- | ------------------- |
| Activo    | TRUE              |
| Stock     | 0                 |
| Descuento | 0                 |
| Total     | 0.00              |

Más adelante también veremos cómo utilizar funciones como `CURRENT_TIMESTAMP` para registrar automáticamente la fecha y hora de creación de un registro.

---

### Casos reales

En aplicaciones empresariales es muy habitual que una gran cantidad de columnas dispongan de valores iniciales.

Esto evita que los desarrolladores tengan que escribir continuamente los mismos datos y reduce la probabilidad de introducir información inconsistente.

Además, centralizar estos valores en la propia base de datos garantiza que cualquier aplicación que utilice el servidor MySQL aplicará exactamente las mismas reglas.

---

### Errores frecuentes

Un error habitual consiste en pensar que `DEFAULT` obliga a utilizar un determinado valor.

En realidad, únicamente proporciona un valor inicial cuando el usuario no especifica otro.

También es frecuente olvidar que el valor por defecto debe ser compatible con el tipo de dato de la columna.

### Ideas clave

* `DEFAULT` permite definir un valor inicial para una columna.
* El valor por defecto solo se utiliza cuando el usuario no proporciona otro.
* Centralizar los valores iniciales en la base de datos mejora la consistencia de la información.
* Los valores por defecto simplifican las operaciones de inserción.
* Durante el resto del curso utilizaremos `DEFAULT` en numerosas tablas del caso práctico.

