# SAVEPOINT

## Introducción

Hasta ahora hemos aprendido que una transacción puede terminar de dos formas:

- Confirmando todos los cambios mediante `COMMIT`.
- Cancelando completamente la operación mediante `ROLLBACK`.

Sin embargo, en muchas aplicaciones reales esto resulta insuficiente.

Imaginemos una transacción formada por veinte operaciones.

Si la operación número diecinueve produce un error, ¿es realmente necesario deshacer también las dieciocho anteriores?

En muchos casos la respuesta es no.

Para resolver este problema existen los **SAVEPOINT**, también conocidos como **puntos de restauración** o **puntos de control**.

Un SAVEPOINT permite crear "marcas" dentro de una transacción para poder retroceder únicamente hasta un punto determinado sin cancelar toda la operación.

## Motivación

Supongamos un proceso de facturación.

Durante una única transacción se realizan las siguientes operaciones:

1. Crear factura.
2. Registrar líneas.
3. Actualizar inventario.
4. Calcular impuestos.
5. Registrar comisión.
6. Generar documento PDF.
7. Enviar correo electrónico.

Si falla el envío del correo electrónico, probablemente no queramos perder todo el trabajo anterior.

Los SAVEPOINT permiten precisamente esa flexibilidad.

## Sintaxis

Crear un punto de restauración.

```sql
SAVEPOINT nombre_punto;
```

Volver a dicho punto.

```sql
ROLLBACK TO SAVEPOINT nombre_punto;
```

Eliminar un punto de restauración.

```sql
RELEASE SAVEPOINT nombre_punto;
```

## Primer ejemplo

```sql
START TRANSACTION;

UPDATE Cuenta
SET Saldo = Saldo - 500
WHERE IdCuenta = 1;

SAVEPOINT despues_descuento;

UPDATE Cuenta
SET Saldo = Saldo + 500
WHERE IdCuenta = 2;

COMMIT;
```

En este caso hemos creado un punto de restauración justo después del primer `UPDATE`.

## Volver a un SAVEPOINT

Supongamos ahora que el segundo `UPDATE` produce un problema.

```sql
START TRANSACTION;

UPDATE Cuenta
SET Saldo = Saldo - 500
WHERE IdCuenta = 1;

SAVEPOINT paso1;

UPDATE Cuenta
SET Saldo = Saldo + 500
WHERE IdCuenta = 2;

ROLLBACK TO SAVEPOINT paso1;

COMMIT;
```

¿Qué ocurre?

El segundo `UPDATE` desaparece.

Sin embargo, el primero continúa formando parte de la transacción.

Esto demuestra que un SAVEPOINT no cancela toda la operación, sino únicamente los cambios posteriores al punto seleccionado.

## Varios SAVEPOINT

Es posible definir tantos puntos de restauración como sean necesarios.

```sql
START TRANSACTION;

INSERT INTO Pedido VALUES (...);

SAVEPOINT pedido_creado;

INSERT INTO DetallePedido VALUES (...);

SAVEPOINT detalles_insertados;

UPDATE Producto
SET Stock = Stock - 3
WHERE IdProducto = 12;

SAVEPOINT stock_actualizado;
```

Si posteriormente ocurre un error, podemos decidir hasta qué punto regresar.

```sql
ROLLBACK TO SAVEPOINT detalles_insertados;
```

Las operaciones posteriores desaparecerán, pero las anteriores seguirán existiendo dentro de la transacción.

## RELEASE SAVEPOINT

Cuando sabemos que un punto de restauración ya no será necesario, podemos eliminarlo.

```sql
RELEASE SAVEPOINT pedido_creado;
```

Esto libera recursos internos.

No afecta a los datos ya modificados.

Simplemente elimina la posibilidad de volver a dicho punto.

## Diferencia entre ROLLBACK y ROLLBACK TO SAVEPOINT

Veamos la diferencia.

```sql
ROLLBACK;
```

Deshace absolutamente toda la transacción.

En cambio:

```sql
ROLLBACK TO SAVEPOINT paso1;
```

Solo elimina las operaciones realizadas después del SAVEPOINT indicado.

La transacción continúa abierta y todavía puede finalizar con `COMMIT`.

## Casos de uso habituales

Los SAVEPOINT son especialmente útiles en:

- Procesos ETL.
- Facturación masiva.
- Importación de datos.
- Procedimientos almacenados complejos.
- Procesos administrativos.
- Migraciones de información.
- Sistemas ERP.

En estos escenarios una operación puede contener decenas o incluso cientos de pasos, y resulta muy útil poder deshacer únicamente una parte del proceso.

## Buenas prácticas

- Utilizar nombres descriptivos para los SAVEPOINT.
- Crear puntos de restauración únicamente cuando aporten valor.
- Eliminar los SAVEPOINT que ya no sean necesarios.
- No abusar de un número excesivo de puntos de restauración.
- Documentar claramente el propósito de cada uno en procedimientos complejos.

## Conclusiones

Los SAVEPOINT proporcionan un control mucho más fino sobre las transacciones. Permiten deshacer únicamente una parte de las operaciones realizadas sin cancelar completamente la transacción, lo que resulta especialmente útil en procesos empresariales complejos con múltiples etapas.

## Ideas clave

- Un SAVEPOINT crea un punto de restauración dentro de una transacción.
- `ROLLBACK TO SAVEPOINT` revierte únicamente los cambios posteriores a dicho punto.
- La transacción continúa abierta tras volver a un SAVEPOINT.
- `RELEASE SAVEPOINT` elimina un punto de restauración que ya no será utilizado.
- Los SAVEPOINT ofrecen un control más preciso que un `ROLLBACK` completo.

