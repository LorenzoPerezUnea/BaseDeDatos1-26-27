# Atomicidad


## Introducción

La primera propiedad de las transacciones recibe el nombre de **Atomicidad** (Atomicity).

Es posiblemente la propiedad más conocida y la más intuitiva de todas.

Cuando los ingenieros diseñaron los primeros sistemas gestores de bases de datos observaron que muchas operaciones debían ejecutarse completamente o no ejecutarse en absoluto.

No existía un punto intermedio aceptable.

La atomicidad nació precisamente para resolver ese problema.

## ¿Qué significa "atómico"?

La palabra **átomo** procede del griego *atomos*, que significa:

> "que no puede dividirse".

Aunque hoy sabemos que los átomos sí pueden dividirse físicamente, el término continúa utilizándose en informática con otro significado.

Una operación atómica es una operación **indivisible**.

No puede quedarse ejecutada a medias.

Solo existen dos estados posibles.

```
No ejecutada
```

o

```
Ejecutada completamente
```

Nunca existe un estado parcial.

## Una analogía sencilla

Imaginemos un interruptor de la luz.

Solo existen dos posiciones.

```
Encendido
```

```
Apagado
```

No existe una posición "medio encendido".

Las transacciones funcionan exactamente igual.

## Aplicación a una transferencia

Recordemos nuestro ejemplo.

```sql
UPDATE Cuenta
SET Saldo = Saldo - 800
WHERE IdCuenta = 1;

UPDATE Cuenta
SET Saldo = Saldo + 800
WHERE IdCuenta = 2;
```

Desde el punto de vista del banco ambas instrucciones representan una única operación.

Por tanto:

- Se ejecutan las dos.
- O no se ejecuta ninguna.

No existe otra posibilidad.

## Una operación compleja

Supongamos ahora un pedido de comercio electrónico.

La compra realiza estas acciones.

```text
Crear pedido

Crear líneas

Actualizar stock

Registrar pago

Actualizar cliente

Registrar auditoría

Generar factura

Actualizar estadísticas
```

Todas pertenecen a una misma unidad lógica.

La atomicidad obliga a que:

```
Todas correctas
```

o

```
Ninguna aplicada
```

## ¿Cómo lo consigue MySQL?

Cuando comienza una transacción, MySQL mantiene un registro interno de los cambios realizados.

Mientras no se confirme la operación:

```
Los cambios permanecen pendientes.
```

Si todo finaliza correctamente:

```
COMMIT
```

Los cambios pasan a ser permanentes.

Si aparece cualquier error:

```
ROLLBACK
```

El motor utiliza esa información para restaurar el estado anterior.

## Ejemplo práctico

Estado inicial.

| Cuenta | Saldo |
|---------|-------:|
| Ana | 5000 |
| Luis | 2500 |

Comienza la transacción.

```sql
START TRANSACTION;
```

Primer cambio.

```sql
UPDATE Cuenta
SET Saldo = Saldo - 800
WHERE IdCuenta = 1;
```

Estado temporal.

| Cuenta | Saldo |
|---------|-------:|
| Ana | 4200 |
| Luis | 2500 |

Ahora ocurre un fallo.

En lugar de confirmar:

```sql
ROLLBACK;
```

Resultado.

| Cuenta | Saldo |
|---------|-------:|
| Ana | 5000 |
| Luis | 2500 |

Todo vuelve al punto inicial.

La operación desaparece completamente.

## ¿Qué pasaría sin atomicidad?

Sin esta propiedad podrían producirse situaciones como:

- Dinero perdido.
- Productos vendidos dos veces.
- Facturas sin pago.
- Pagos sin factura.
- Reservas incompletas.
- Inventarios negativos.
- Registros huérfanos.

Todos ellos representan estados imposibles para el negocio.

## Atomicidad y procedimientos almacenados

Es habitual que un procedimiento almacenado ejecute decenas de instrucciones.

```sql
CALL RegistrarPedido(...);
```

Desde la aplicación solo vemos una llamada.

Sin embargo, internamente puede ejecutar:

- INSERT.
- UPDATE.
- DELETE.
- Validaciones.
- Consultas.
- Cálculos.

Todas ellas deberían ejecutarse dentro de una misma transacción para conservar la atomicidad.

## Buenas prácticas

- Considerar siempre la operación desde el punto de vista del negocio y no de las sentencias SQL individuales.
- Agrupar únicamente las instrucciones que formen una unidad lógica.
- Evitar dejar transacciones abiertas durante mucho tiempo.
- Gestionar correctamente los errores para asegurar un ROLLBACK cuando sea necesario.
- Diseñar procedimientos almacenados teniendo presente esta propiedad.

## Conclusiones

La atomicidad garantiza que una transacción sea tratada como una unidad indivisible de trabajo. Gracias a ella, una base de datos nunca queda en un estado parcialmente actualizado, evitando inconsistencias que podrían tener consecuencias graves para el funcionamiento de una aplicación.

## Ideas clave

- Atómico significa indivisible.
- Una transacción nunca queda a medias.
- Solo existen dos resultados: todo o nada.
- COMMIT confirma todos los cambios.
- ROLLBACK deshace completamente la operación.
- La atomicidad es la primera propiedad del modelo ACID.

