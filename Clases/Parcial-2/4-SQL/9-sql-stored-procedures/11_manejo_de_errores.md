# Manejo de errores

## Introducción

En cualquier aplicación pueden producirse errores durante la ejecución de un procedimiento.

Por ejemplo:

* intentar insertar un cliente duplicado;
* consultar un registro que no existe;
* violar una clave foránea;
* producir una división entre cero;
* recibir parámetros incorrectos.

Si no gestionamos estas situaciones, el procedimiento finalizará con un error que será devuelto a la aplicación.

Para controlar estos casos, MySQL incorpora mecanismos básicos de ​**manejo de errores**​.

---

## ¿Por qué es importante?

Imaginemos un procedimiento que registra una venta.

Las operaciones son:

1. Insertar el pedido.
2. Actualizar el stock.
3. Registrar la factura.

¿Qué ocurre si el segundo paso falla?

Sin un tratamiento adecuado podríamos terminar con:

* un pedido registrado;
* un stock incorrecto;
* una factura inexistente.

El sistema quedaría en un estado inconsistente.

En clases posteriores veremos cómo las **transacciones** ayudan a resolver este problema. De momento aprenderemos a detectar y controlar errores.

---

## DECLARE HANDLER

MySQL utiliza la instrucción:

```sql
DECLARE ... HANDLER
```

para indicar qué debe hacerse cuando ocurre un error.

La forma más sencilla es:

```sql
DECLARE EXIT HANDLER
FOR SQLEXCEPTION

BEGIN

    SELECT 'Ha ocurrido un error.';

END;
```

Este bloque se ejecutará automáticamente si aparece cualquier excepción durante el procedimiento.

---

## Primer ejemplo

```sql
DELIMITER $$

CREATE PROCEDURE EjemploError()

BEGIN

    DECLARE EXIT HANDLER
    FOR SQLEXCEPTION

    BEGIN

        SELECT 'Se produjo un error durante la ejecución.';

    END;

    SELECT 10 / 0;

END $$

DELIMITER ;
```

Al producirse el error, el procedimiento no finalizará abruptamente, sino que ejecutará el bloque definido por el manejador.

---

## Tipos de manejadores

Los más utilizados son:

### EXIT

Finaliza inmediatamente el procedimiento cuando ocurre el error.

```text
Error

↓

Ejecutar HANDLER

↓

Salir del procedimiento
```

---

### CONTINUE

Permite continuar la ejecución después de tratar el error.

```text
Error

↓

Ejecutar HANDLER

↓

Continuar
```

Debe utilizarse con cuidado, ya que continuar tras un error puede producir resultados inesperados.

---

## Un ejemplo práctico

Supongamos que queremos buscar un cliente.

```sql
DECLARE EXIT HANDLER
FOR NOT FOUND

BEGIN

    SELECT 'Cliente no encontrado';

END;
```

Este tipo de manejador es muy habitual cuando trabajamos con cursores.

---

## ¿Qué errores pueden controlarse?

Entre otros:

* `SQLEXCEPTION`: cualquier excepción SQL.
* `SQLWARNING`: advertencias.
* `NOT FOUND`: no se encontró ningún registro.

Estos tres tipos cubren la mayoría de situaciones habituales.

---

## Recomendaciones

Aunque MySQL permite capturar errores, no debemos utilizar los manejadores como sustituto de una buena validación.

Siempre es preferible comprobar previamente:

* que el cliente existe;
* que el stock es suficiente;
* que los parámetros son válidos.

Gestionar un error es útil, pero prevenirlo suele ser una mejor estrategia.

---

## Buenas prácticas

* Declara los manejadores al principio del procedimiento.
* Utiliza mensajes claros durante el desarrollo.
* Valida los datos antes de ejecutar operaciones críticas.
* Reserva `CONTINUE` para situaciones justificadas.
* Combina el manejo de errores con transacciones cuando trabajes con operaciones importantes.

---

## Ideas clave

* Los errores pueden gestionarse mediante `DECLARE HANDLER`.
* Los manejadores permiten controlar el comportamiento del procedimiento ante una excepción.
* `EXIT` finaliza el procedimiento.
* `CONTINUE` permite seguir ejecutándolo.
* Un buen manejo de errores mejora la robustez y la fiabilidad de las aplicaciones.

