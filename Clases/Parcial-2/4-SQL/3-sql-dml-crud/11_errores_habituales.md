# Errores habituales

## Introducción

Durante las primeras prácticas con SQL es completamente normal cometer errores.

La mayoría de ellos no se deben a problemas de sintaxis complejos, sino a pequeños descuidos que terminan provocando resultados inesperados o mensajes de error.

Conocer los fallos más frecuentes permitirá detectarlos rápidamente y desarrollar una metodología de trabajo mucho más segura.

---

## Error 1. No indicar las columnas

Aunque MySQL permite escribir:

```sql
INSERT INTO Cliente
VALUES (...);
```

esta práctica no es recomendable.

Si en el futuro cambia el orden de las columnas o se añade una nueva, el código dejará de funcionar correctamente.

La forma recomendada es:

```sql
INSERT INTO Cliente
(
    Nombre,
    CorreoElectronico,
    Ciudad
)
VALUES
(
    'Ana',
    'ana@empresa.com',
    'Santander'
);
```

---

## Error 2. Número incorrecto de valores

Cada columna debe recibir exactamente un valor.

Por ejemplo:

```sql
INSERT INTO Categoria
(
    Nombre,
    Descripcion
)
VALUES
(
    'Portátiles'
);
```

Esta sentencia producirá un error porque falta el valor correspondiente a `Descripcion`.

---

## Error 3. Tipos de datos incompatibles

Cada columna espera un tipo de dato determinado.

Por ejemplo:

```sql
INSERT INTO Producto
(
    Precio
)
VALUES
(
    'Mucho'
);
```

Una columna numérica no puede almacenar una cadena de texto.

---

## Error 4. Olvidar WHERE en UPDATE

Este es uno de los errores más peligrosos.

```sql
UPDATE Producto

SET Precio = 0;
```

Todos los productos quedarán con precio cero.

Siempre debe revisarse cuidadosamente la condición antes de ejecutar una actualización.

---

## Error 5. Olvidar WHERE en DELETE

Situación similar.

```sql
DELETE FROM Cliente;
```

Todos los clientes desaparecerán.

La tabla seguirá existiendo, pero vacía.

---

## Error 6. Violar restricciones

Muchos errores aparecen al incumplir alguna restricción:

* duplicar una clave primaria;
* repetir un valor `UNIQUE`;
* utilizar una clave foránea inexistente;
* insertar un valor `NULL` donde no está permitido;
* incumplir una condición `CHECK`.

Cuando aparezca un mensaje de error, la primera tarea debe consistir en identificar qué restricción está siendo violada.

---

## Error 7. No comprobar el resultado

Después de cada operación DML conviene ejecutar una consulta para verificar el efecto producido.

Durante las primeras prácticas utilizaremos continuamente:

```sql
SELECT *
FROM NombreTabla;
```

Este sencillo hábito evita muchos problemas y facilita enormemente la depuración.

---

## Buenas prácticas

Antes de ejecutar cualquier modificación importante conviene seguir una pequeña lista de comprobación:

* revisar la sintaxis;
* comprobar la lista de columnas;
* verificar los tipos de datos;
* confirmar la condición `WHERE`;
* ejecutar un `SELECT` previo si es necesario;
* revisar el resultado después de la operación.

Estos pasos apenas requieren unos segundos y reducen enormemente la probabilidad de cometer errores.

---

## Ideas clave

* La mayoría de los errores se deben a pequeños descuidos.
* Indicar siempre las columnas hace el código más robusto.
* Revisar `WHERE` es obligatorio antes de ejecutar `UPDATE` o `DELETE`.
* Las restricciones ayudan a detectar datos incorrectos.
* Verificar el resultado forma parte del trabajo habitual con SQL.

