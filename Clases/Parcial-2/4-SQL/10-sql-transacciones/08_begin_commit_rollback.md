# BEGIN, COMMIT y ROLLBACK

## Introducción

Hasta ahora hemos estudiado qué son las transacciones y cuáles son las propiedades que deben cumplir. A partir de este punto comenzaremos a trabajar con las instrucciones SQL que permiten controlarlas.

En MySQL, el ciclo de vida de una transacción gira alrededor de tres instrucciones fundamentales:

- `START TRANSACTION` (o `BEGIN`)
- `COMMIT`
- `ROLLBACK`

Estas instrucciones permiten indicar al SGBD cuándo comienza una unidad lógica de trabajo, cuándo debe hacerse permanente y cuándo debe deshacerse por completo.

Comprender correctamente estas órdenes es imprescindible antes de estudiar temas más avanzados como los puntos de restauración (SAVEPOINT), los niveles de aislamiento o el control de concurrencia.

## ¿Qué es una transacción?

Una transacción es un conjunto de una o más instrucciones SQL que deben ejecutarse como una única operación lógica.

Conceptualmente, el ciclo completo puede representarse así:

```text
Inicio

↓

Ejecutar operaciones SQL

↓

¿Todo correcto?

↓              ↓

Sí             No

↓              ↓

COMMIT     ROLLBACK
```

Mientras la transacción permanezca abierta, los cambios aún no son permanentes.

## START TRANSACTION

La instrucción `START TRANSACTION` indica a MySQL que todas las sentencias posteriores formarán parte de la misma transacción hasta que ésta finalice.

Su sintaxis es:

```sql
START TRANSACTION;
```

También puede utilizarse el sinónimo:

```sql
BEGIN;
```

Ambas instrucciones tienen el mismo efecto en MySQL.

A partir de ese momento, cualquier operación de inserción, modificación o eliminación quedará pendiente de confirmación.

## Primer ejemplo

Supongamos la siguiente tabla.

```sql
CREATE TABLE Producto (

    IdProducto INT PRIMARY KEY,

    Nombre VARCHAR(100),

    Stock INT

);
```

Insertamos algunos registros.

```sql
INSERT INTO Producto VALUES
(1,'Portátil',10),
(2,'Monitor',8);
```

Ahora comenzamos una transacción.

```sql
START TRANSACTION;
```

Reducimos el stock.

```sql
UPDATE Producto
SET Stock = Stock - 2
WHERE IdProducto = 1;
```

Si consultamos desde la misma sesión:

```sql
SELECT *
FROM Producto;
```

obtendremos:

| Producto | Stock |
|-----------|------:|
| Portátil | 8 |
| Monitor | 8 |

Sin embargo, esos cambios todavía no son permanentes.

## COMMIT

Cuando todas las operaciones han finalizado correctamente, utilizamos:

```sql
COMMIT;
```

Esta instrucción confirma la transacción.

A partir de ese momento:

- Los cambios pasan a ser permanentes.
- Otros usuarios podrán observarlos según el nivel de aislamiento correspondiente.
- MySQL garantiza su durabilidad.

Ejemplo completo.

```sql
START TRANSACTION;

UPDATE Producto
SET Stock = Stock - 2
WHERE IdProducto = 1;

COMMIT;
```

Tras ejecutar `COMMIT`, el nuevo stock queda almacenado definitivamente.

## ROLLBACK

Si durante la ejecución detectamos cualquier error, podemos cancelar toda la operación mediante:

```sql
ROLLBACK;
```

Esta instrucción deshace todas las modificaciones realizadas desde el inicio de la transacción.

Ejemplo.

```sql
START TRANSACTION;

UPDATE Producto
SET Stock = Stock - 2
WHERE IdProducto = 1;

ROLLBACK;
```

Tras el `ROLLBACK`, la tabla vuelve exactamente al estado anterior.

## Ejemplo de transferencia bancaria

```sql
START TRANSACTION;

UPDATE Cuenta
SET Saldo = Saldo - 1000
WHERE IdCuenta = 1;

UPDATE Cuenta
SET Saldo = Saldo + 1000
WHERE IdCuenta = 2;

COMMIT;
```

Si cualquiera de las dos actualizaciones produce un error:

```sql
START TRANSACTION;

UPDATE Cuenta
SET Saldo = Saldo - 1000
WHERE IdCuenta = 1;

-- Error detectado

ROLLBACK;
```

La cuenta recuperará automáticamente su saldo original.

## ¿Qué ocurre si olvido hacer COMMIT?

Es un error relativamente frecuente.

Mientras la transacción permanezca abierta:

- Los cambios siguen siendo temporales.
- Pueden mantenerse bloqueos sobre determinados registros.
- Otros usuarios podrían quedar esperando.
- Si la conexión finaliza inesperadamente, normalmente MySQL ejecutará un `ROLLBACK` automático.

Por ello es importante cerrar siempre las transacciones correctamente.

## ¿Puede haber varias transacciones abiertas?

Cada conexión mantiene su propia transacción.

Dos usuarios distintos pueden ejecutar:

```sql
START TRANSACTION;
```

de manera simultánea.

Cada uno trabajará sobre su propio contexto transaccional.

El motor será el encargado de coordinar ambas operaciones.

## Autocommit

Por defecto, MySQL trabaja en modo **autocommit**.

Esto significa que cada sentencia SQL constituye automáticamente una transacción independiente.

Por ejemplo:

```sql
UPDATE Producto
SET Stock = 12
WHERE IdProducto = 1;
```

Finaliza automáticamente con un `COMMIT`.

Podemos comprobar el estado mediante:

```sql
SELECT @@autocommit;
```

Y modificarlo temporalmente.

```sql
SET autocommit = 0;
```

Cuando el autocommit está desactivado, el programador debe confirmar manualmente cada transacción.

## Buenas prácticas

- Mantener las transacciones lo más cortas posible.
- Confirmar únicamente cuando todas las validaciones hayan terminado.
- Cancelar inmediatamente al detectar cualquier error.
- Evitar realizar operaciones interactivas mientras una transacción permanece abierta.
- No olvidar nunca ejecutar `COMMIT` o `ROLLBACK`.

## Conclusiones

`START TRANSACTION`, `COMMIT` y `ROLLBACK` constituyen las tres instrucciones fundamentales para trabajar con transacciones en MySQL. Permiten agrupar múltiples operaciones en una única unidad lógica y decidir si los cambios deben hacerse permanentes o deshacerse completamente.

## Ideas clave

- `START TRANSACTION` inicia una transacción.
- `BEGIN` es un sinónimo de `START TRANSACTION`.
- `COMMIT` confirma definitivamente los cambios.
- `ROLLBACK` deshace todas las modificaciones pendientes.
- Una transacción siempre debe finalizar correctamente mediante `COMMIT` o `ROLLBACK`.

