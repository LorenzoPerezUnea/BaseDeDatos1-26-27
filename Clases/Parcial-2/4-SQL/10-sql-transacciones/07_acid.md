# Propiedades ACID

## Introducción

Las transacciones constituyen uno de los pilares fundamentales de las bases de datos relacionales modernas. Sin embargo, para comprender realmente su funcionamiento es necesario estudiar las cuatro propiedades que deben cumplir.

Estas propiedades fueron definidas para garantizar que una transacción sea fiable, segura y capaz de mantener la integridad de la información incluso en situaciones adversas.

El conjunto de estas cuatro propiedades recibe el nombre de **ACID**, un acrónimo formado por las iniciales de:

- **A**tomicity (Atomicidad)
- **C**onsistency (Consistencia)
- **I**solation (Aislamiento)
- **D**urability (Durabilidad)

Aunque cada propiedad tiene un objetivo específico, todas trabajan conjuntamente. Una transacción solo puede considerarse correcta cuando satisface las cuatro.

## Visión global

Podemos interpretar ACID como un conjunto de garantías que ofrece el sistema gestor de bases de datos.

```text
ACID
              │
 ┌────────────┼────────────┐
 │            │            │
Atomicidad Consistencia Aislamiento Durabilidad
```

Cada una responde a una pregunta distinta.

| Propiedad | Pregunta que responde |
|-----------|-----------------------|
| Atomicidad | ¿Se ejecuta toda la operación? |
| Consistencia | ¿Los datos siguen siendo válidos? |
| Aislamiento | ¿Las transacciones interfieren entre sí? |
| Durabilidad | ¿Se conservarán los cambios tras un fallo? |

## Atomicidad

La atomicidad considera una transacción como una única unidad de trabajo.

No admite resultados parciales.

Si cualquiera de las instrucciones falla, todas las modificaciones realizadas hasta ese momento deben deshacerse.

Su lema es:

> Todo o nada.

## Consistencia

La consistencia garantiza que todas las restricciones y reglas del modelo continúan siendo válidas una vez finalizada la transacción.

Una base de datos consistente nunca contiene estados imposibles.

Por ejemplo:

- claves duplicadas,
- referencias inexistentes,
- saldos inválidos,
- reglas de negocio incumplidas.

## Aislamiento

El aislamiento permite que cientos o miles de usuarios trabajen simultáneamente sobre la misma base de datos sin interferir entre sí.

Cada transacción debe comportarse como si fuese la única que está utilizando el sistema.

Dependiendo del nivel de aislamiento elegido, el SGBD permitirá distintos grados de concurrencia.

## Durabilidad

La durabilidad asegura que una vez confirmado un `COMMIT`, los cambios permanecerán almacenados incluso si el servidor falla inmediatamente después.

Es la propiedad que proporciona confianza al usuario en que una operación confirmada nunca desaparecerá.

## ¿Qué ocurre si falta una propiedad?

Si eliminamos cualquiera de las cuatro propiedades, aparecen problemas importantes.

Sin atomicidad:

- operaciones incompletas.

Sin consistencia:

- datos contradictorios.

Sin aislamiento:

- conflictos entre usuarios.

Sin durabilidad:

- pérdida de información tras un fallo.

Por ello, las cuatro propiedades son imprescindibles y deben entenderse como un conjunto inseparable.

## ACID en MySQL

El motor **InnoDB** implementa el modelo ACID mediante diversos mecanismos internos.

Entre ellos destacan:

- Transacciones.
- Bloqueos.
- MVCC (Multi-Version Concurrency Control).
- Undo Log.
- Redo Log.
- Recuperación automática.
- Restricciones de integridad.

Gracias a esta combinación, MySQL puede mantener la fiabilidad de la información incluso en sistemas con miles de operaciones concurrentes.

## Ejemplo completo

Consideremos una transferencia bancaria.

```sql
START TRANSACTION;

UPDATE Cuenta
SET Saldo = Saldo - 500
WHERE IdCuenta = 1;

UPDATE Cuenta
SET Saldo = Saldo + 500
WHERE IdCuenta = 2;

COMMIT;
```

Durante esta operación:

- **Atomicidad** garantiza que ambas actualizaciones se ejecuten juntas.
- **Consistencia** mantiene válido el saldo total del sistema.
- **Aislamiento** evita interferencias con otras transferencias simultáneas.
- **Durabilidad** asegura que el resultado permanezca almacenado tras el `COMMIT`.

## Buenas prácticas

- Utilizar siempre motores transaccionales.
- Diseñar operaciones siguiendo una única unidad lógica.
- Confirmar únicamente cuando todas las validaciones hayan finalizado.
- Comprender el efecto de los niveles de aislamiento.
- No abusar de transacciones excesivamente largas.

## Conclusiones

El modelo ACID constituye uno de los elementos diferenciadores de los sistemas gestores de bases de datos relacionales. Gracias a estas cuatro propiedades, es posible construir aplicaciones capaces de gestionar información crítica con un elevado nivel de fiabilidad, incluso en entornos con miles de usuarios concurrentes y fallos inesperados.

## Ideas clave

- ACID resume las cuatro propiedades fundamentales de una transacción.
- Las cuatro trabajan conjuntamente.
- El motor InnoDB implementa estas garantías en MySQL.
- Sin alguna de ellas aparecerían inconsistencias o pérdidas de información.
- Comprender ACID es esencial para diseñar aplicaciones robustas.

