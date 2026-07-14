# Aislamiento


## Introducción

Hasta ahora hemos supuesto que únicamente existe un usuario utilizando la base de datos.

Sin embargo, esa situación casi nunca ocurre en sistemas reales.

Una tienda online puede tener miles de compradores al mismo tiempo.

Un banco puede recibir decenas de miles de operaciones por segundo.

Una red social puede almacenar millones de publicaciones simultáneamente.

Todos esos usuarios están leyendo y modificando las mismas tablas.

La propiedad **Aislamiento (Isolation)** existe para evitar que las operaciones de unos usuarios interfieran con las de otros.

## El problema de la concurrencia

Supongamos una cuenta bancaria.

| Cuenta | Saldo |
|---------|-------:|
| Ana | 5000 |

Dos cajeros realizan operaciones exactamente al mismo tiempo.

El primero intenta retirar:

```
500 €
```

El segundo intenta retirar:

```
1000 €
```

Ambos leen inicialmente:

```
Saldo = 5000
```

Si trabajan sin aislamiento podrían sobrescribirse mutuamente.

El resultado dependería del orden de ejecución.

Incluso podrían perderse modificaciones.

## ¿Qué significa aislar una transacción?

Una transacción debe comportarse como si fuera la única que está utilizando la base de datos.

Aunque internamente cientos de usuarios estén trabajando simultáneamente, cada uno debe obtener resultados coherentes.

El usuario nunca debería observar cambios parciales realizados por otros usuarios.

## Analogía

Imaginemos una biblioteca.

Cada investigador consulta un libro en una mesa independiente.

Mientras uno está revisando el contenido, otro investigador no debería arrancar páginas del mismo libro.

Primero termina uno.

Después continúa el siguiente.

Así se evita trabajar con información incompleta.

## Un ejemplo práctico

Supongamos dos sesiones distintas.

**Sesión A**

```sql
START TRANSACTION;

UPDATE Cuenta
SET Saldo = Saldo - 1000
WHERE IdCuenta = 1;
```

Todavía no ejecuta:

```sql
COMMIT;
```

Mientras tanto aparece otra conexión.

**Sesión B**

```sql
SELECT Saldo
FROM Cuenta
WHERE IdCuenta = 1;
```

La gran pregunta es:

¿Qué saldo debería ver?

¿El antiguo?

¿El nuevo?

¿Depende del nivel de aislamiento?

Precisamente para responder a estas preguntas existen los distintos niveles de aislamiento que estudiaremos más adelante.

## ¿Por qué no mostrar siempre el cambio inmediatamente?

Supongamos que la primera transacción finalmente falla.

```sql
ROLLBACK;
```

Si otros usuarios hubiesen visto el nuevo saldo antes del rollback, habrían trabajado con información que realmente nunca existió.

Esto produciría decisiones incorrectas.

## El coste del aislamiento

Mantener las transacciones completamente aisladas tiene un coste.

Mientras una transacción modifica determinados registros:

- otras pueden esperar,
- algunas consultas pueden bloquearse,
- disminuye el paralelismo,
- aumenta el tiempo de respuesta.

Existe por tanto un equilibrio entre:

- rendimiento,
- seguridad,
- consistencia.

Por esta razón los SGBD ofrecen varios niveles de aislamiento.

## ¿Cómo consigue MySQL el aislamiento?

El motor InnoDB utiliza diferentes mecanismos.

Entre ellos:

- bloqueos de filas,
- bloqueos compartidos,
- bloqueos exclusivos,
- versiones de registros (MVCC),
- control de concurrencia,
- registros Undo.

Dependiendo del nivel de aislamiento configurado utilizará unos mecanismos u otros.

## Un ejemplo cotidiano

Imaginemos una hoja de cálculo compartida.

Si diez personas modifican simultáneamente la misma celda sin coordinación, el resultado será impredecible.

En cambio, si únicamente una persona puede modificar esa celda mientras el resto espera o trabaja con una copia consistente, se evita el conflicto.

Ese es precisamente el objetivo del aislamiento.

## ¿Siempre interesa el máximo aislamiento?

No necesariamente.

Cuanto mayor sea el aislamiento:

- mayor seguridad,
- menos inconsistencias,

pero también:

- más bloqueos,
- menor concurrencia,
- menor rendimiento.

Cada aplicación debe elegir el nivel adecuado según sus necesidades.

## Buenas prácticas

- Mantener las transacciones lo más cortas posible.
- Evitar operaciones innecesarias dentro de una transacción.
- Elegir el nivel de aislamiento apropiado.
- Diseñar aplicaciones preparadas para trabajar con concurrencia.
- Comprender que varios usuarios pueden acceder simultáneamente a los mismos datos.

## Conclusiones

El aislamiento permite que múltiples usuarios trabajen simultáneamente sobre una misma base de datos sin interferir entre sí. Gracias a esta propiedad, cada transacción observa una visión coherente de la información y evita leer cambios incompletos o inconsistentes realizados por otras transacciones. Es una de las características que hacen posible el funcionamiento fiable de los sistemas multiusuario modernos.

## Ideas clave

- En sistemas reales existen muchas transacciones simultáneas.
- El aislamiento evita interferencias entre ellas.
- Cada transacción trabaja sobre una visión coherente de los datos.
- Mayor aislamiento implica mayor seguridad, pero también más coste.
- MySQL implementa distintos niveles de aislamiento para adaptarse a diferentes escenarios.

