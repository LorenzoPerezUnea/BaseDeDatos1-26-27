# MODIFY COLUMN

## Introducción

Añadir nuevas columnas no es la única modificación que puede experimentar una base de datos a lo largo de su vida.

También es frecuente descubrir que una columna ya existente necesita cambiar.

Quizá inicialmente reservamos 50 caracteres para almacenar el nombre de un producto y, tras varios meses de uso, comprobamos que ese límite resulta insuficiente.

O quizá una columna definida como `INT` deba convertirse en `BIGINT` porque el volumen de datos ha crecido mucho más de lo esperado.

En estos casos no es necesario eliminar la columna y volver a crearla.

MySQL permite modificar su definición mediante la cláusula ​**MODIFY COLUMN**​.

---

### ¿Cuándo utilizar MODIFY COLUMN?

`MODIFY COLUMN` permite cambiar las características de una columna existente.

Entre las modificaciones más habituales se encuentran:

* cambiar el tipo de dato;
* aumentar la longitud de un `VARCHAR`;
* añadir o eliminar `NOT NULL`;
* modificar un valor `DEFAULT`.

Es importante tener en cuenta que estas operaciones pueden afectar a los datos ya almacenados, por lo que deben realizarse con precaución.

---

### Sintaxis general

La estructura básica es:

```sql
ALTER TABLE NombreTabla
MODIFY COLUMN NombreColumna NuevoTipo;
```

Al utilizar `MODIFY COLUMN` debemos especificar nuevamente la definición completa de la columna.

Por ejemplo, si una columna era `VARCHAR(100) NOT NULL`, al modificar su longitud también deberemos volver a indicar `NOT NULL`.

---

### Primer ejemplo

Supongamos que el campo `Nombre` de la tabla `Producto` resulta demasiado corto.

Inicialmente estaba definido como:

```sql
Nombre VARCHAR(120) NOT NULL
```

Queremos ampliarlo a 200 caracteres.

Ejecutaremos:

```sql
ALTER TABLE Producto
MODIFY COLUMN Nombre VARCHAR(200) NOT NULL;
```

La estructura de la tabla cambiará sin afectar al contenido ya almacenado.

---

### Verificando el resultado

Después de cualquier modificación estructural debemos comprobar el resultado.

```sql
DESC Producto;
```

Observaremos que la longitud máxima permitida para la columna `Nombre` ha cambiado.

También podemos consultar la definición completa.

```sql
SHOW CREATE TABLE Producto;
```

Esta segunda consulta resulta especialmente útil para comprobar restricciones y propiedades adicionales.

---

### Cambiando un valor por defecto

`MODIFY COLUMN` también permite modificar un valor `DEFAULT`.

Por ejemplo:

```sql
ALTER TABLE Producto
MODIFY COLUMN Stock INT DEFAULT 10;
```

A partir de este momento, todos los nuevos productos comenzarán con diez unidades de stock cuando no se indique otro valor.

Los registros existentes no se modificarán.

---

### Precauciones

Modificar el tipo de una columna puede provocar pérdidas de información si el nuevo tipo admite menos datos que el anterior.

Por ejemplo, reducir un `VARCHAR(200)` a `VARCHAR(50)` podría truncar valores existentes.

Antes de realizar este tipo de operaciones conviene analizar cuidadosamente la información almacenada y, en entornos profesionales, realizar copias de seguridad.

---

### Casos reales

Durante la evolución de una aplicación es habitual modificar columnas para:

* ampliar el tamaño de campos de texto;
* cambiar restricciones;
* adaptar tipos de datos a nuevos requisitos;
* mejorar el rendimiento del almacenamiento.

Estas modificaciones forman parte del mantenimiento normal de cualquier base de datos empresarial.

---

### Errores frecuentes

Uno de los errores más habituales consiste en olvidar repetir la definición completa de la columna al utilizar `MODIFY COLUMN`.

También es frecuente reducir el tamaño de una columna sin comprobar previamente los datos existentes.

Finalmente, muchos estudiantes modifican la estructura sin verificar posteriormente el resultado mediante `DESC`.

### Ideas clave

* `MODIFY COLUMN` permite cambiar la definición de una columna existente.
* Debe especificarse nuevamente la definición completa de la columna.
* Puede utilizarse para modificar tipos de datos, restricciones y valores por defecto.
* Las modificaciones deben realizarse con precaución cuando existen datos almacenados.
* Verificar siempre el resultado forma parte de las buenas prácticas profesionales.

