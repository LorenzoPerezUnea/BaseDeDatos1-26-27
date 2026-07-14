# Niveles de aislamiento

## Introducción

En el apartado anterior aprendimos que el aislamiento es una de las cuatro propiedades ACID y que su objetivo es impedir que varias transacciones interfieran entre sí.

Sin embargo, conseguir un aislamiento absoluto tiene un coste importante.

Si cada transacción bloqueara completamente toda la base de datos hasta finalizar, los sistemas serían extremadamente lentos y apenas podrían atender usuarios simultáneamente.

Por otro lado, si todas las transacciones pudieran acceder libremente a los mismos datos al mismo tiempo, aparecerían inconsistencias y resultados impredecibles.

Existe, por tanto, un compromiso entre dos objetivos contrapuestos:

- Mantener la consistencia de la información.
- Maximizar el rendimiento y la concurrencia.

Para resolver este problema, el estándar SQL define distintos **niveles de aislamiento**. Cada uno establece qué fenómenos de concurrencia están permitidos y cuáles deben evitarse.

MySQL implementa estos niveles mediante el motor de almacenamiento InnoDB.

## ¿Por qué existen varios niveles?

Imaginemos dos aplicaciones completamente distintas.

La primera es un sistema bancario que gestiona millones de euros cada día.

La segunda es una página web de noticias donde miles de usuarios consultan artículos.

En el banco es preferible sacrificar algo de rendimiento para asegurar que ninguna operación produzca inconsistencias.

En cambio, en la página de noticias resulta más importante atender muchas consultas rápidamente que impedir pequeñas diferencias temporales en los datos mostrados.

Ambos sistemas utilizan bases de datos relacionales, pero sus necesidades son diferentes.

Los niveles de aislamiento permiten adaptar el comportamiento del SGBD a cada escenario.

## Los cuatro niveles definidos por el estándar SQL

El estándar SQL define cuatro niveles principales.

| Nivel | Protección ofrecida |
|--------|---------------------|
| READ UNCOMMITTED | Mínima protección |
| READ COMMITTED | Evita lecturas sucias |
| REPEATABLE READ | Evita lecturas no repetibles |
| SERIALIZABLE | Máxima protección |

Cada nivel añade nuevas garantías respecto al anterior.

A cambio, también aumenta el número de bloqueos y disminuye la concurrencia.

## READ UNCOMMITTED

Es el nivel de aislamiento más bajo.

Permite que una transacción lea cambios realizados por otra transacción aunque todavía no hayan sido confirmados mediante `COMMIT`.

Esto significa que una consulta podría mostrar datos que posteriormente desaparecerán porque la otra transacción ejecutó un `ROLLBACK`.

Por este motivo apenas se utiliza en sistemas críticos.

Ejemplo conceptual:

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

Con READ UNCOMMITTED podría obtener:

```
1000
```

Aunque ese valor todavía no sea definitivo.

## READ COMMITTED

En este nivel únicamente pueden leerse datos ya confirmados.

Si una transacción todavía no ha ejecutado `COMMIT`, sus modificaciones permanecen invisibles para el resto.

Este comportamiento evita las llamadas **lecturas sucias (Dirty Reads)**.

Es el nivel utilizado por defecto en sistemas como Oracle o Microsoft SQL Server.

## REPEATABLE READ

Este nivel añade una garantía adicional.

Una vez que una transacción lee un registro, volverá a obtener exactamente el mismo resultado durante toda la transacción, aunque otro usuario modifique posteriormente dicho registro.

MySQL utiliza este nivel como configuración predeterminada para InnoDB.

Gracias al mecanismo MVCC (Multi-Version Concurrency Control), el motor puede ofrecer una visión consistente de los datos sin bloquear innecesariamente todas las consultas.

## SERIALIZABLE

Es el nivel de aislamiento más estricto.

Las transacciones se comportan como si se ejecutaran una detrás de otra.

Aunque varios usuarios trabajen simultáneamente, el resultado será equivalente a una ejecución completamente secuencial.

Este nivel elimina prácticamente todos los problemas de concurrencia, pero reduce considerablemente el rendimiento.

Se utiliza únicamente en operaciones extremadamente críticas.

## Cambiar el nivel de aislamiento

Podemos consultar el nivel actual mediante:

```sql
SELECT @@transaction_isolation;
```

También es posible modificarlo para la sesión actual.

```sql
SET SESSION TRANSACTION ISOLATION LEVEL READ COMMITTED;
```

O establecerlo antes de iniciar una transacción.

```sql
SET TRANSACTION ISOLATION LEVEL SERIALIZABLE;

START TRANSACTION;
```

## Comparativa

| Nivel | Rendimiento | Seguridad |
|--------|------------:|-----------|
| READ UNCOMMITTED | Muy alto | Muy baja |
| READ COMMITTED | Alto | Buena |
| REPEATABLE READ | Medio | Muy buena |
| SERIALIZABLE | Bajo | Máxima |

Como puede observarse, no existe un nivel perfecto.

Cada aplicación debe elegir el más adecuado según sus necesidades.

## ¿Cuál utiliza MySQL?

En el motor InnoDB el nivel predeterminado es:

```
REPEATABLE READ
```

Este nivel proporciona un excelente equilibrio entre rendimiento y consistencia, razón por la cual ha sido elegido como configuración por defecto.

No obstante, en determinadas aplicaciones puede resultar conveniente utilizar un nivel diferente.

## Buenas prácticas

- Utilizar el nivel predeterminado salvo que exista una necesidad concreta.
- Comprender el impacto de cada nivel antes de modificarlo.
- No elegir SERIALIZABLE únicamente por "mayor seguridad".
- Probar siempre el comportamiento de la aplicación bajo concurrencia real.
- Documentar cualquier cambio en el nivel de aislamiento.

## Conclusiones

Los niveles de aislamiento permiten ajustar el equilibrio entre rendimiento y consistencia. Cada uno controla qué interacciones pueden producirse entre transacciones concurrentes y qué problemas deben evitarse. Elegir el nivel adecuado constituye una decisión de diseño importante en cualquier aplicación empresarial.

## Ideas clave

- No todas las aplicaciones necesitan el mismo nivel de aislamiento.
- Un mayor aislamiento implica normalmente menor concurrencia.
- MySQL utiliza REPEATABLE READ como nivel predeterminado.
- El nivel puede configurarse para cada sesión o transacción.
- Elegir correctamente el nivel mejora tanto la seguridad como el rendimiento.

