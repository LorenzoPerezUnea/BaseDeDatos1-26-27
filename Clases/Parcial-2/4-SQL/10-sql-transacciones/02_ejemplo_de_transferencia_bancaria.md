
# Ejemplo de transferencia bancaria

## Introducción

A lo largo de esta clase utilizaremos repetidamente un ejemplo muy sencillo pero extremadamente representativo: una transferencia bancaria.

Aunque pueda parecer un caso específico del sector financiero, en realidad representa un patrón que aparece en prácticamente cualquier aplicación empresarial.

Una transferencia consiste en mover un recurso desde un origen hasta un destino.

Ese recurso puede ser:

- Dinero.
- Stock.
- Créditos.
- Puntos de fidelización.
- Entradas para un concierto.
- Plazas en un curso.
- Habitaciones de un hotel.
- Asientos de un avión.

En todos los casos aparece el mismo requisito:

**Nunca debe perderse ni duplicarse el recurso durante la operación.**

Este ejemplo servirá para comprender cómo funcionan internamente las transacciones y por qué son imprescindibles.

## El escenario

Supongamos una base de datos muy sencilla.

```sql
CREATE TABLE Cuenta (
    IdCuenta INT PRIMARY KEY,
    Titular VARCHAR(100),
    Saldo DECIMAL(10,2)
);
```

Insertamos algunos datos.

```sql
INSERT INTO Cuenta VALUES
(1,'Ana',5000.00),
(2,'Luis',2500.00),
(3,'Empresa',15000.00);
```

Estado inicial:

| Cuenta | Titular | Saldo |
|---------|----------|-------:|
| 1 | Ana | 5000.00 |
| 2 | Luis | 2500.00 |
| 3 | Empresa | 15000.00 |

Ana desea transferir 800 € a Luis.

A simple vista parece una única operación.

Sin embargo, internamente implica varias acciones.

## Paso 1. Comprobar que la cuenta existe

Antes de modificar nada debemos asegurarnos de que la cuenta origen existe.

```sql
SELECT *
FROM Cuenta
WHERE IdCuenta = 1;
```

También verificamos la cuenta destino.

```sql
SELECT *
FROM Cuenta
WHERE IdCuenta = 2;
```

Si alguna no existe, la operación debe cancelarse.

## Paso 2. Comprobar saldo suficiente

No tendría sentido permitir una transferencia imposible.

```sql
SELECT Saldo
FROM Cuenta
WHERE IdCuenta = 1;
```

Supongamos que el saldo es:

```
5000 €
```

Como queremos transferir:

```
800 €
```

La operación puede continuar.

## Paso 3. Descontar el dinero

La primera modificación consiste en reducir el saldo de la cuenta origen.

```sql
UPDATE Cuenta
SET Saldo = Saldo - 800
WHERE IdCuenta = 1;
```

Ahora la tabla queda así.

| Cuenta | Saldo |
|---------|-------:|
| Ana | 4200 |
| Luis | 2500 |

Todavía falta una parte importante.

## Paso 4. Ingresar el dinero

```sql
UPDATE Cuenta
SET Saldo = Saldo + 800
WHERE IdCuenta = 2;
```

Resultado.

| Cuenta | Saldo |
|---------|-------:|
| Ana | 4200 |
| Luis | 3300 |

Ahora sí la operación está completa.

## ¿Qué ocurre si aparece un error?

Supongamos que el servidor falla después del primer UPDATE.

Solo se ejecuta esto.

```sql
UPDATE Cuenta
SET Saldo = Saldo - 800
WHERE IdCuenta = 1;
```

Pero nunca llega a ejecutarse el segundo.

El resultado sería:

| Cuenta | Saldo |
|---------|-------:|
| Ana | 4200 |
| Luis | 2500 |

¿Dónde están los 800 €?

Han desaparecido.

La base de datos ha quedado inconsistente.

## El problema aumenta con sistemas reales

En un banco moderno una transferencia no implica únicamente dos UPDATE.

Puede incluir:

- Actualizar saldo.
- Registrar movimiento.
- Crear justificante.
- Actualizar libro contable.
- Registrar comisión.
- Actualizar estadísticas.
- Enviar notificación.
- Actualizar auditoría.
- Registrar impuestos.
- Actualizar balances diarios.

Es habitual que una única transferencia implique entre diez y treinta instrucciones SQL.

Sin transacciones sería prácticamente imposible garantizar que todas se ejecutan correctamente.

## La solución

Las transacciones permiten agrupar todas esas instrucciones.

Visualmente podríamos representarlo así.

```
Inicio

↓

Comprobar cuentas

↓

Comprobar saldo

↓

Descontar dinero

↓

Ingresar dinero

↓

Registrar movimiento

↓

Registrar auditoría

↓

Actualizar estadísticas

↓

Confirmar
```

Si cualquiera de esos pasos falla:

```
Cancelar toda la operación
```

Como si nunca hubiera comenzado.

## Implementación con transacciones

La transferencia anterior puede escribirse así.

```sql
START TRANSACTION;

UPDATE Cuenta
SET Saldo = Saldo - 800
WHERE IdCuenta = 1;

UPDATE Cuenta
SET Saldo = Saldo + 800
WHERE IdCuenta = 2;

COMMIT;
```

Ahora ambas operaciones forman una única unidad lógica.

## ¿Y si ocurre un error?

Si detectamos cualquier problema:

```sql
START TRANSACTION;

UPDATE Cuenta
SET Saldo = Saldo - 800
WHERE IdCuenta = 1;

ROLLBACK;
```

Después del ROLLBACK el saldo vuelve exactamente al estado inicial.

La actualización desaparece.

Es como si nunca hubiese ocurrido.

## Una analogía útil

Imaginemos que escribimos un documento de cien páginas.

Mientras trabajamos realizamos cientos de cambios.

Solo cuando pulsamos **Guardar** los cambios pasan a ser permanentes.

Si el programa se bloquea antes de guardar, normalmente todo vuelve al último estado guardado.

Las transacciones funcionan de forma muy parecida.

Mientras no exista un COMMIT, los cambios permanecen pendientes.

Solo al confirmar pasan a formar parte permanente de la base de datos.

## Buenas prácticas

- Validar todos los datos antes de modificar información.
- Mantener la transacción abierta el menor tiempo posible.
- Confirmar únicamente cuando todas las operaciones hayan finalizado correctamente.
- Cancelar inmediatamente ante cualquier error.
- Registrar todas las operaciones críticas para facilitar auditorías.

## Conclusiones

La transferencia bancaria constituye uno de los ejemplos clásicos para estudiar las transacciones porque muestra claramente que una única operación de negocio suele estar formada por múltiples instrucciones SQL. Si cualquiera de ellas falla, toda la operación pierde sentido. Gracias a las transacciones, MySQL puede garantizar que el dinero nunca desaparezca ni aparezca de forma incorrecta.

## Ideas clave

- Una transferencia es una única operación lógica.
- Internamente ejecuta múltiples sentencias SQL.
- Todas deben completarse correctamente.
- Si una falla, deben deshacerse todas.
- Este patrón aparece en casi cualquier sistema empresarial.

