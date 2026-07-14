# Caso práctico empresarial

## Introducción

A lo largo de esta clase hemos estudiado los conceptos teóricos relacionados con las transacciones: las propiedades ACID, el uso de `START TRANSACTION`, `COMMIT`, `ROLLBACK`, los puntos de restauración y los niveles de aislamiento.

En este apartado reuniremos todos esos conceptos en un caso práctico inspirado en una situación empresarial real.

Trabajaremos con la empresa ficticia utilizada durante todo el curso, dedicada a la venta de productos informáticos.

Cuando un cliente realiza un pedido, el sistema debe ejecutar numerosas operaciones relacionadas entre sí. Si cualquiera de ellas falla, toda la operación debe cancelarse para evitar inconsistencias.

Este escenario refleja el funcionamiento habitual de un ERP o de una plataforma de comercio electrónico.

## Escenario

La empresa dispone de las siguientes tablas simplificadas.

```sql
Cliente
```

```text
IdCliente
Nombre
SaldoPendiente
```

```sql
Producto
```

```text
IdProducto
Nombre
Stock
Precio
```

```sql
Pedido
```

```text
IdPedido
IdCliente
Fecha
Estado
Total
```

```sql
DetallePedido
```

```text
IdDetalle
IdPedido
IdProducto
Cantidad
PrecioUnitario
```

```sql
MovimientoInventario
```

```text
IdMovimiento
IdProducto
Cantidad
Tipo
Fecha
```

## Objetivo

Un cliente desea comprar:

- 2 portátiles.
- 1 monitor.
- 3 teclados.

El sistema debe realizar todas las operaciones necesarias para registrar correctamente la compra.

## Flujo del proceso

Desde el punto de vista del negocio, la operación puede representarse así.

```text
Comprobar cliente

↓

Comprobar stock

↓

Crear pedido

↓

Insertar líneas

↓

Actualizar inventario

↓

Registrar movimientos

↓

Actualizar importe

↓

Confirmar transacción
```

Aunque el usuario solo pulsa el botón **Comprar**, internamente se ejecutan numerosas instrucciones SQL.

## Paso 1. Iniciar la transacción

```sql
START TRANSACTION;
```

A partir de este momento todas las operaciones formarán parte de la misma unidad lógica.

## Paso 2. Verificar el cliente

Antes de registrar un pedido debemos comprobar que el cliente existe.

```sql
SELECT IdCliente
FROM Cliente
WHERE IdCliente = 25;
```

En una aplicación real también podrían verificarse aspectos como:

- Cliente activo.
- Sin bloqueos administrativos.
- Sin límite de crédito superado.
- Sin incidencias de pago.

Si alguna comprobación falla, se ejecutará:

```sql
ROLLBACK;
```

## Paso 3. Comprobar el stock

```sql
SELECT Stock
FROM Producto
WHERE IdProducto = 10;
```

Supongamos que el resultado es:

```
Stock = 15
```

Como el pedido solicita únicamente dos unidades, la operación puede continuar.

Esta comprobación debe repetirse para todos los productos del pedido.

## Paso 4. Crear el pedido

```sql
INSERT INTO Pedido
(
    IdCliente,
    Fecha,
    Estado,
    Total
)
VALUES
(
    25,
    NOW(),
    'Pendiente',
    0
);
```

Recuperamos el identificador generado.

```sql
SET @IdPedido = LAST_INSERT_ID();
```

## Paso 5. Insertar las líneas del pedido

```sql
INSERT INTO DetallePedido
(
    IdPedido,
    IdProducto,
    Cantidad,
    PrecioUnitario
)
VALUES
(@IdPedido,10,2,950.00);
```

Se repite la operación para cada producto adquirido.

## Paso 6. Actualizar el inventario

```sql
UPDATE Producto
SET Stock = Stock - 2
WHERE IdProducto = 10;
```

Después se actualizan el resto de productos.

## Paso 7. Registrar el movimiento de almacén

```sql
INSERT INTO MovimientoInventario
(
    IdProducto,
    Cantidad,
    Tipo,
    Fecha
)
VALUES
(
    10,
    -2,
    'VENTA',
    NOW()
);
```

Gracias a esta tabla será posible reconstruir posteriormente todos los movimientos del inventario.

## Paso 8. Calcular el importe total

Una vez insertadas todas las líneas podemos calcular el importe del pedido.

```sql
UPDATE Pedido
SET Total =
(
    SELECT SUM(Cantidad * PrecioUnitario)
    FROM DetallePedido
    WHERE IdPedido = @IdPedido
)
WHERE IdPedido = @IdPedido;
```

## Paso 9. Confirmar la operación

Si todas las instrucciones anteriores finalizan correctamente:

```sql
COMMIT;
```

En ese instante:

- El pedido queda registrado.
- El inventario queda actualizado.
- Los movimientos quedan almacenados.
- Los cambios pasan a ser permanentes.

## ¿Qué ocurre si aparece un error?

Supongamos que durante la actualización del inventario se detecta un problema.

Por ejemplo:

- Stock insuficiente.
- Error de conexión.
- Restricción violada.
- Error interno del procedimiento.

En ese caso bastará ejecutar:

```sql
ROLLBACK;
```

El resultado será:

- El pedido desaparecerá.
- Las líneas desaparecerán.
- El inventario volverá a su estado original.
- No quedarán movimientos registrados.

La base de datos permanecerá exactamente igual que antes de iniciar la operación.

## ¿Y si utilizamos SAVEPOINT?

Imaginemos ahora que deseamos conservar parte del trabajo realizado.

```sql
START TRANSACTION;

INSERT INTO Pedido (...);

SAVEPOINT pedido_creado;

INSERT INTO DetallePedido (...);

UPDATE Producto
SET Stock = Stock - 2
WHERE IdProducto = 10;
```

Si únicamente falla la actualización del inventario:

```sql
ROLLBACK TO SAVEPOINT pedido_creado;
```

Las operaciones posteriores al SAVEPOINT desaparecerán, mientras que las anteriores continuarán existiendo dentro de la transacción.

Finalmente podremos decidir si completar el proceso o cancelar toda la operación.

## Aplicaciones reales

Este patrón aparece continuamente en aplicaciones empresariales.

Por ejemplo:

- Venta de productos.
- Pago de facturas.
- Reserva de habitaciones.
- Compra de entradas.
- Matrícula universitaria.
- Gestión de nóminas.
- Transferencias bancarias.
- Control de inventario.
- Facturación electrónica.
- Sistemas ERP.

En todos estos casos una única acción del usuario implica múltiples modificaciones sobre distintas tablas.

## Buenas prácticas

- Iniciar la transacción lo más tarde posible.
- Finalizarla lo antes posible.
- Validar previamente todos los datos.
- Evitar operaciones lentas dentro de la transacción.
- Registrar adecuadamente los errores.
- Utilizar `ROLLBACK` ante cualquier situación inesperada.
- Diseñar procedimientos almacenados que agrupen toda la lógica de negocio.

## Conclusiones

Las transacciones permiten implementar procesos empresariales complejos con un elevado nivel de seguridad. Gracias a ellas es posible coordinar múltiples modificaciones sobre distintas tablas y garantizar que todas se completen correctamente o, en caso contrario, que ninguna llegue a aplicarse.

## Ideas clave

- Una operación empresarial suele afectar a múltiples tablas.
- Todas las modificaciones deben formar parte de la misma transacción.
- `COMMIT` confirma definitivamente el proceso.
- `ROLLBACK` restaura el estado inicial.
- Las transacciones son uno de los pilares de cualquier aplicación profesional basada en bases de datos.

