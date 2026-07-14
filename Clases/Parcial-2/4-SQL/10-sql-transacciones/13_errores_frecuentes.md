# Errores frecuentes

## Introducción

Las transacciones son uno de los mecanismos más importantes de un sistema gestor de bases de datos, pero también uno de los que generan más errores entre estudiantes y desarrolladores con poca experiencia.

Muchos de estos errores no producen mensajes de error inmediatos. En su lugar, generan problemas de consistencia, bloqueos o pérdidas de rendimiento que solo se detectan cuando la aplicación comienza a utilizarse de forma intensiva.

En este apartado revisaremos los errores más habituales relacionados con el uso de transacciones y aprenderemos cómo evitarlos.

## Error 1. No utilizar transacciones

Es el error más grave y, desgraciadamente, uno de los más comunes.

Muchos principiantes escriben varias instrucciones SQL consecutivas sin agruparlas dentro de una transacción.

Por ejemplo:

```sql
UPDATE Cuenta
SET Saldo = Saldo - 500
WHERE IdCuenta = 1;

UPDATE Cuenta
SET Saldo = Saldo + 500
WHERE IdCuenta = 2;
```

Si la segunda instrucción falla, la primera ya habrá modificado la base de datos.

La operación quedará incompleta.

**Cómo evitarlo**

Siempre que varias instrucciones formen una única operación lógica, deben ejecutarse dentro de una transacción.

```sql
START TRANSACTION;

...

COMMIT;
```

## Error 2. Olvidar el COMMIT

Otro error muy frecuente consiste en iniciar una transacción y olvidar confirmarla.

```sql
START TRANSACTION;

UPDATE Producto
SET Stock = Stock - 5
WHERE IdProducto = 10;
```

Si nunca se ejecuta:

```sql
COMMIT;
```

los cambios permanecerán pendientes.

Dependiendo del cliente utilizado, al cerrar la conexión MySQL ejecutará automáticamente un `ROLLBACK`.

El usuario creerá que la operación se realizó correctamente cuando, en realidad, no se almacenó ningún cambio.

## Error 3. No gestionar errores

Muchas aplicaciones realizan un `COMMIT` independientemente de que hayan ocurrido errores.

Este comportamiento puede dejar la base de datos en un estado inconsistente.

Siempre debe comprobarse el resultado de cada operación antes de confirmar la transacción.

Si aparece cualquier incidencia, lo correcto es ejecutar:

```sql
ROLLBACK;
```

## Error 4. Mantener transacciones abiertas demasiado tiempo

Una transacción abierta mantiene recursos ocupados.

Por ejemplo:

- Bloqueos.
- Versiones de registros.
- Información en los logs.
- Memoria interna.

Si permanece abierta durante varios minutos puede afectar al rendimiento de otros usuarios.

**Incorrecto**

```text
START TRANSACTION

↓

Modificar datos

↓

Esperar respuesta del usuario

↓

Seguir trabajando

↓

COMMIT
```

Mientras el usuario piensa qué hacer, la transacción continúa abierta.

**Correcto**

Primero recopilar toda la información necesaria.

Después iniciar la transacción.

Finalmente confirmar o cancelar inmediatamente.

## Error 5. Mezclar operaciones lentas

Dentro de una transacción no deberían realizarse tareas como:

- Esperar peticiones HTTP.
- Enviar correos electrónicos.
- Generar informes extensos.
- Procesar archivos muy grandes.
- Solicitar confirmaciones al usuario.

Estas operaciones aumentan innecesariamente la duración de la transacción.

## Error 6. Elegir un nivel de aislamiento inadecuado

Seleccionar siempre el nivel `SERIALIZABLE` pensando que es "el mejor" puede provocar un descenso importante del rendimiento.

Del mismo modo, utilizar `READ UNCOMMITTED` en un sistema bancario sería una decisión muy peligrosa.

Cada aplicación debe elegir el nivel de aislamiento que mejor se adapte a sus necesidades.

## Error 7. Confiar únicamente en la aplicación

Las reglas críticas no deberían depender exclusivamente del código de la aplicación.

Siempre que sea posible conviene apoyarse también en:

- Restricciones.
- Claves foráneas.
- CHECK.
- Procedimientos almacenados.
- Triggers.

De esta forma la propia base de datos ayuda a mantener la consistencia.

## Error 8. No pensar en la concurrencia

Durante el desarrollo es habitual probar una aplicación con un único usuario.

Sin embargo, en producción cientos de usuarios pueden acceder simultáneamente a la misma información.

Una operación aparentemente correcta puede fallar cuando varias transacciones se ejecutan al mismo tiempo.

Por ello es recomendable realizar pruebas de concurrencia antes de poner una aplicación en funcionamiento.

## Error 9. Utilizar motores no transaccionales

No todos los motores de almacenamiento soportan transacciones.

Por ejemplo, el antiguo motor MyISAM no implementa las propiedades ACID.

Si se necesita trabajar con transacciones, debe utilizarse un motor como InnoDB.

## Error 10. No documentar la lógica transaccional

En proyectos grandes es habitual encontrar procedimientos almacenados con decenas de instrucciones SQL.

Si no se documenta claramente:

- dónde comienza la transacción,
- cuándo se confirma,
- cuándo se cancela,

el mantenimiento del sistema se vuelve mucho más complejo.

## Recomendaciones generales

Antes de implementar una transacción conviene responder a las siguientes preguntas:

- ¿Qué operación de negocio representa?
- ¿Qué instrucciones forman realmente parte de ella?
- ¿Qué ocurre si una falla?
- ¿Debe deshacerse todo o solo una parte?
- ¿Es necesario utilizar SAVEPOINT?
- ¿Qué nivel de aislamiento resulta adecuado?

Responder a estas cuestiones ayuda a diseñar transacciones más robustas y fáciles de mantener.

## Conclusiones

La mayoría de los problemas relacionados con las transacciones no se deben a errores de sintaxis, sino a decisiones de diseño. Comprender cómo funcionan las propiedades ACID, los mecanismos de concurrencia y las herramientas que ofrece MySQL permite desarrollar aplicaciones mucho más fiables y resistentes frente a fallos.

## Ideas clave

- No todas las operaciones necesitan una transacción, pero las operaciones críticas sí.
- Nunca debe olvidarse finalizar una transacción con `COMMIT` o `ROLLBACK`.
- Las transacciones deben ser cortas y bien definidas.
- Elegir correctamente el nivel de aislamiento es una decisión de diseño.
- La planificación y la documentación son tan importantes como la sintaxis SQL.

