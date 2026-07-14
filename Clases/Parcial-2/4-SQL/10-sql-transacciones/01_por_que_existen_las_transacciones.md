# ¿Por qué existen las transacciones?

## Introducción

Cuando comenzamos a estudiar SQL, la mayoría de los ejemplos consistían en ejecutar una única instrucción:

```sql
INSERT INTO Cliente (...);
```

o

```sql
UPDATE Producto
SET Stock = Stock - 1
WHERE IdProducto = 5;
```

Estas operaciones parecen sencillas y normalmente funcionan correctamente.

Sin embargo, los sistemas reales rara vez realizan una única operación aislada.

Una compra online puede implicar decenas de modificaciones distintas.

Una transferencia bancaria puede modificar varias tablas.

Una matrícula universitaria puede actualizar alumnos, asignaturas, pagos y plazas disponibles.

Todas estas operaciones deben ejecutarse como una única unidad lógica.

Ahí es donde aparecen las transacciones.

## El problema de las operaciones múltiples

Supongamos que una tienda online recibe un pedido.

El proceso podría consistir en:

1. Crear el pedido.
2. Registrar sus líneas.
3. Descontar stock.
4. Actualizar ventas.
5. Registrar el pago.
6. Generar la factura.
7. Registrar un movimiento contable.

Aunque para el usuario parece una única acción ("Comprar"), internamente la base de datos ejecuta numerosas instrucciones SQL.

```text
INSERT Pedido

INSERT DetallePedido

UPDATE Producto

INSERT Factura

INSERT Pago

UPDATE Cliente

INSERT MovimientoContable
```

¿Qué ocurre si el servidor falla justo después del tercer paso?

El resultado sería un sistema incoherente.

## Un ejemplo sin transacciones

Supongamos una base de datos bancaria.

Tabla Cuenta

| Cuenta | Saldo |
|---------|------:|
| A | 5000 |
| B | 2000 |

Queremos transferir 1000 € desde A hacia B.

Primera operación:

```sql
UPDATE Cuenta
SET Saldo = Saldo - 1000
WHERE Cuenta='A';
```

Estado:

| Cuenta | Saldo |
|---------|------:|
| A | 4000 |
| B | 2000 |

Hasta aquí todo parece correcto.

Ahora debería ejecutarse:

```sql
UPDATE Cuenta
SET Saldo = Saldo + 1000
WHERE Cuenta='B';
```

Pero justo antes...

- se apaga el servidor
- falla el disco
- se pierde la conexión
- se reinicia el sistema operativo

La segunda sentencia nunca llega a ejecutarse.

Resultado final:

| Cuenta | Saldo |
|---------|------:|
| A | 4000 |
| B | 2000 |

Los 1000 € han desaparecido.

La base de datos ha quedado en un estado imposible desde el punto de vista del negocio.

## El problema no es SQL

Es importante comprender que SQL ha ejecutado correctamente la primera instrucción.

No existe ningún error de sintaxis.

El problema es que la operación completa requería varias instrucciones relacionadas entre sí.

La base de datos necesita tratarlas como si fueran una única operación indivisible.

## ¿Qué significa "todo o nada"?

Las transacciones siguen una filosofía muy sencilla:

> O bien se ejecutan todas las operaciones, o no se ejecuta ninguna.

No existe un punto intermedio.

Es exactamente igual que firmar un contrato.

Un contrato no puede quedar firmado únicamente por una de las partes.

O ambas firman, o el contrato no existe.

Las transacciones funcionan de forma análoga.

## Una analogía cotidiana

Imaginemos un cajero automático.

Cuando retiramos dinero ocurren muchas acciones:

1. Comprobar la tarjeta.
2. Verificar el PIN.
3. Consultar saldo.
4. Descontar dinero.
5. Registrar el movimiento.
6. Expulsar el efectivo.
7. Imprimir el recibo.

Todas ellas forman una única operación lógica.

Si el cajero detecta un fallo antes de entregar el dinero, debe cancelar toda la operación.

Nunca debería descontar dinero sin entregarlo.

## Sistemas donde las transacciones son imprescindibles

Las transacciones son esenciales en prácticamente cualquier sistema empresarial:

- Bancos.
- Hospitales.
- Comercio electrónico.
- Sistemas de reservas.
- Gestión de inventarios.
- ERP.
- Nóminas.
- Facturación.
- Contabilidad.
- Gestión tributaria.
- Universidades.
- Aerolíneas.

En todos ellos un pequeño error puede traducirse en pérdidas económicas importantes o información inconsistente.

## ¿Qué aporta una transacción?

Una transacción permite agrupar varias instrucciones SQL para que el motor de base de datos las trate como una sola unidad de trabajo.

Desde el punto de vista del usuario, la operación será indivisible.

Solo existen dos resultados posibles:

- Todo se ejecuta correctamente.
- Nada cambia en la base de datos.

Este comportamiento garantiza que la información permanezca coherente incluso ante fallos inesperados.

## Buenas prácticas

- Identificar qué operaciones pertenecen a una misma unidad lógica.
- Mantener las transacciones lo más breves posible.
- Evitar realizar tareas innecesarias dentro de una transacción.
- Confirmar únicamente cuando todas las validaciones hayan finalizado con éxito.
- Cancelar inmediatamente si se detecta cualquier error.

## Conclusiones

Las transacciones no son un mecanismo opcional, sino una necesidad en cualquier aplicación que manipule información crítica. Permiten convertir múltiples instrucciones SQL en una única operación coherente y segura, evitando estados intermedios inválidos y garantizando que la base de datos permanezca consistente incluso ante errores o fallos del sistema.

## Ideas clave

- Una operación empresarial suele implicar varias instrucciones SQL.
- Ejecutarlas por separado puede producir inconsistencias.
- Las transacciones agrupan todas esas instrucciones.
- Su filosofía es "todo o nada".
- Constituyen la base de la fiabilidad de un SGBD moderno.

