# UPDATE

## Introducción

Insertar registros constituye únicamente una parte del trabajo diario con una base de datos.

Con el paso del tiempo la información cambia continuamente.

Los clientes modifican su dirección de correo.

Los productos cambian de precio.

Los empleados son ascendidos.

El stock aumenta tras una compra o disminuye después de una venta.

Todas estas operaciones requieren modificar registros ya existentes.

Para ello utilizaremos la sentencia ​**UPDATE**​.

---

## ¿Qué hace UPDATE?

`UPDATE` modifica uno o varios registros de una tabla.

A diferencia de `INSERT`, no crea nuevas filas.

Simplemente cambia el contenido de las ya existentes.

Visualmente:

```text
Antes

Producto

Precio = 1299.95

↓

UPDATE

↓

Producto

Precio = 1199.95
```

El registro sigue siendo el mismo.

Únicamente cambia parte de su información.

---

## Sintaxis general

La estructura básica es:

```sql
UPDATE NombreTabla

SET
    Columna = Valor

WHERE Condición;
```

La cláusula `SET` indica qué columnas se modificarán.

La cláusula `WHERE` determina qué registros sufrirán el cambio.

---

## Primer ejemplo

Supongamos que deseamos actualizar el precio de un producto.

```sql
UPDATE Producto

SET
    Precio = 1199.95

WHERE
    IdProducto = 1;
```

Solo se modificará el producto cuyo identificador sea 1.

Todos los demás permanecerán sin cambios.

---

## Modificando varias columnas

Podemos actualizar varios atributos simultáneamente.

```sql
UPDATE Cliente

SET
    Ciudad = 'Bilbao',
    Activo = FALSE

WHERE
    IdCliente = 3;
```

Las dos modificaciones se realizan como una única operación.

---

## Verificando el resultado

Después de cualquier actualización debemos comprobar el efecto obtenido.

```sql
SELECT *
FROM Producto
WHERE IdProducto = 1;
```

La consulta mostrará el nuevo precio almacenado.

Verificar los cambios constituye una buena práctica profesional.

---

## Actualizaciones masivas

También es posible modificar muchos registros simultáneamente.

Por ejemplo:

```sql
UPDATE Producto

SET
    Activo = FALSE

WHERE
    Stock = 0;
```

Todos los productos sin existencias pasarán automáticamente a estado inactivo.

Este tipo de operaciones resulta muy habitual en sistemas empresariales.

---

## La importancia del WHERE

En todos los ejemplos anteriores aparece la cláusula `WHERE`.

No es casualidad.

Si olvidamos escribirla, ​**MySQL modificará absolutamente todos los registros de la tabla**​.

Por ejemplo:

```sql
UPDATE Producto

SET
    Precio = 0;
```

Esta sentencia establecería el precio de todos los productos en cero.

Por ello dedicaremos un capítulo completo a estudiar la importancia de `WHERE`.

---

## Casos reales

`UPDATE` aparece continuamente en aplicaciones reales.

Por ejemplo:

* modificar un correo electrónico;
* actualizar un precio;
* registrar un cambio de stock;
* activar o desactivar usuarios;
* actualizar puntos de fidelización.

Cada modificación realizada por un usuario termina convirtiéndose en una sentencia muy similar a las estudiadas aquí.

---

## Errores frecuentes

El error más grave consiste en olvidar la cláusula `WHERE`.

También es frecuente utilizar una condición demasiado amplia y modificar más registros de los previstos.

Antes de ejecutar un `UPDATE` conviene revisar cuidadosamente la condición utilizada.

### Ideas clave

* `UPDATE` modifica registros existentes.
* La cláusula `SET` indica qué columnas cambian.
* `WHERE` determina qué filas serán modificadas.
* Puede actualizar una o varias columnas simultáneamente.
* Olvidar `WHERE` constituye uno de los errores más peligrosos al trabajar con SQL.

