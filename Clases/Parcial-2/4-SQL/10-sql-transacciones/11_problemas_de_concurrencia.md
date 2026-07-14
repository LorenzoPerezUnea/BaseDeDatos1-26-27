# Problemas de concurrencia

## Introducción

Ahora que conocemos los niveles de aislamiento, es el momento de estudiar los problemas que intentan resolver.

Cuando varias transacciones acceden simultáneamente a los mismos datos pueden producirse situaciones inesperadas.

Estos problemas reciben el nombre de **fenómenos de concurrencia**.

Comprenderlos resulta fundamental para entender por qué existen distintos niveles de aislamiento y por qué el motor de base de datos necesita mecanismos como bloqueos, versiones de registros o control de concurrencia.

En este apartado estudiaremos los problemas más importantes definidos por el estándar SQL.

## ¿Qué es la concurrencia?

Existe concurrencia cuando varias transacciones trabajan al mismo tiempo sobre la misma base de datos.

Por ejemplo:

- Dos cajeros modifican la misma cuenta bancaria.
- Dos empleados venden el último producto disponible.
- Dos administradores editan el mismo registro.
- Miles de usuarios reservan entradas para un concierto.

Sin mecanismos de control, estas operaciones pueden producir resultados incorrectos.

## Lectura sucia (Dirty Read)

Una lectura sucia ocurre cuando una transacción lee datos que todavía no han sido confirmados.

Ejemplo.

**Sesión A**

```sql
START TRANSACTION;

UPDATE Cuenta
SET Saldo = 1000
WHERE IdCuenta = 1;
```

Todavía no ejecuta:

```sql
COMMIT;
```

Mientras tanto:

**Sesión B**

```sql
SELECT Saldo
FROM Cuenta
WHERE IdCuenta = 1;
```

Obtiene:

```
1000
```

Posteriormente:

**Sesión A**

```sql
ROLLBACK;
```

El saldo vuelve a su valor original.

La sesión B ha trabajado con información que realmente nunca existió.

## Lectura no repetible (Non-Repeatable Read)

Este problema aparece cuando una misma consulta devuelve resultados distintos dentro de una misma transacción.

Ejemplo.

**Sesión A**

```sql
START TRANSACTION;

SELECT Saldo
FROM Cuenta
WHERE IdCuenta = 1;
```

Resultado.

```
5000
```

Mientras tanto:

**Sesión B**

```sql
UPDATE Cuenta
SET Saldo = 4500
WHERE IdCuenta = 1;

COMMIT;
```

La sesión A vuelve a ejecutar exactamente la misma consulta.

```sql
SELECT Saldo
FROM Cuenta
WHERE IdCuenta = 1;
```

Ahora obtiene:

```
4500
```

La misma consulta ha producido dos resultados distintos.

## Lectura fantasma (Phantom Read)

En este caso no cambia un registro existente.

Lo que cambia es el conjunto de registros devueltos.

Ejemplo.

```sql
SELECT *
FROM Pedido
WHERE Estado = 'Pendiente';
```

La consulta devuelve:

```
15 pedidos
```

Mientras la transacción continúa abierta, otro usuario inserta un nuevo pedido pendiente.

```sql
INSERT INTO Pedido (...)
VALUES (...);

COMMIT;
```

Al repetir la consulta aparecen:

```
16 pedidos
```

Ha aparecido un "registro fantasma".

## Actualización perdida (Lost Update)

Este problema no forma parte del estándar SQL original, pero es uno de los conflictos más frecuentes en aplicaciones reales.

Dos usuarios leen el mismo valor inicial.

```
Stock = 20
```

El primer usuario vende dos unidades.

```
20 → 18
```

El segundo usuario vende cinco unidades utilizando todavía el valor antiguo.

```
20 → 15
```

El resultado correcto debería haber sido:

```
13
```

Sin embargo, uno de los cambios sobrescribe al otro.

Se ha perdido una actualización.

## Resumen de los problemas

| Problema | Consecuencia |
|----------|--------------|
| Dirty Read | Leer datos no confirmados |
| Non-Repeatable Read | La misma consulta devuelve valores distintos |
| Phantom Read | Cambia el número de registros obtenidos |
| Lost Update | Una modificación sobrescribe otra |

## Relación con los niveles de aislamiento

Cada nivel evita determinados problemas.

| Nivel | Dirty | Non-Repeatable | Phantom |
|--------|:-----:|:--------------:|:-------:|
| READ UNCOMMITTED | ❌ | ❌ | ❌ |
| READ COMMITTED | ✅ | ❌ | ❌ |
| REPEATABLE READ | ✅ | ✅ | ❌* |
| SERIALIZABLE | ✅ | ✅ | ✅ |

> *En MySQL InnoDB, gracias a MVCC y a los bloqueos de siguiente clave (Next-Key Locks), muchos casos de lecturas fantasma también quedan evitados, aunque el estándar SQL únicamente garantiza su eliminación completa en SERIALIZABLE.

## ¿Cómo evita MySQL estos problemas?

InnoDB combina diversos mecanismos internos.

Entre ellos:

- MVCC.
- Undo Log.
- Redo Log.
- Bloqueos compartidos.
- Bloqueos exclusivos.
- Next-Key Locks.
- Gap Locks.

La combinación de estas técnicas permite mantener un alto nivel de concurrencia sin sacrificar la consistencia de la información.

Estos mecanismos serán estudiados con mayor profundidad en clases posteriores dedicadas al funcionamiento interno del SGBD.

## Buenas prácticas

- Diseñar las transacciones pensando en la concurrencia.
- Evitar mantener bloqueos más tiempo del necesario.
- Elegir correctamente el nivel de aislamiento.
- Probar aplicaciones con múltiples usuarios simultáneos.
- No asumir que una consulta devolverá siempre el mismo resultado en cualquier contexto.

## Conclusiones

Los problemas de concurrencia aparecen cuando varias transacciones interactúan simultáneamente sobre los mismos datos. Comprender fenómenos como las lecturas sucias, las lecturas no repetibles o las lecturas fantasma permite diseñar aplicaciones más robustas y elegir correctamente el nivel de aislamiento adecuado para cada situación.

## Ideas clave

- La concurrencia es inevitable en sistemas multiusuario.
- Existen varios fenómenos clásicos definidos por el estándar SQL.
- Los niveles de aislamiento intentan evitar estos problemas.
- MySQL utiliza múltiples mecanismos internos para gestionar la concurrencia.
- Comprender estos fenómenos es esencial para desarrollar aplicaciones seguras.

