# Parámetros de salida

## Introducción

En el apartado anterior aprendimos a enviar información **hacia** un procedimiento mediante parámetros `IN`.

Sin embargo, en muchas ocasiones también necesitamos que el procedimiento **devuelva información** al programa que lo ha llamado.

Para ello MySQL dispone de los ​**parámetros de salida (`OUT`)**​.

Mientras que un parámetro `IN` actúa como una entrada, un parámetro `OUT` actúa como una salida del procedimiento.

---

## Parámetros OUT

La sintaxis general es:

```sql
CREATE PROCEDURE NombreProcedimiento(

    OUT parametro TipoDato

)
```

Durante la ejecución del procedimiento podremos asignar un valor a ese parámetro.

Al finalizar, dicho valor será devuelto al programa que realizó la llamada.

---

## Primer ejemplo

Queremos conocer el número total de clientes registrados.

```sql
DELIMITER $$

CREATE PROCEDURE ContarClientes(

    OUT pTotal INT

)

BEGIN

    SELECT COUNT(*)
    INTO pTotal
    FROM Cliente;

END $$

DELIMITER ;
```

Observa una instrucción nueva:

```sql
SELECT ... INTO
```

Esta permite almacenar el resultado de una consulta dentro de una variable o parámetro.

---

## Ejecutar el procedimiento

Antes de llamar al procedimiento necesitamos una variable de sesión.

```sql
SET @TotalClientes = 0;
```

Después ejecutamos:

```sql
CALL ContarClientes(@TotalClientes);
```

Y finalmente consultamos el valor devuelto.

```sql
SELECT @TotalClientes;
```

Resultado:

```text
125
```

(El valor dependerá de los datos existentes en la base de datos.)

---

## Parámetros IN y OUT simultáneamente

Un procedimiento puede recibir información y devolver un resultado.

Por ejemplo:

```sql
DELIMITER $$

CREATE PROCEDURE ContarPedidosCliente(

    IN pIdCliente INT,
    OUT pCantidad INT

)

BEGIN

    SELECT COUNT(*)
    INTO pCantidad
    FROM Pedido
    WHERE IdCliente = pIdCliente;

END $$

DELIMITER ;
```

Llamada:

```sql
SET @Pedidos = 0;

CALL ContarPedidosCliente(3, @Pedidos);

SELECT @Pedidos;
```

---

## ¿Cuándo utilizar OUT?

Los parámetros de salida son útiles cuando queremos devolver:

* un contador;
* un importe calculado;
* una fecha;
* un identificador generado;
* cualquier otro valor único.

Si necesitamos devolver muchas filas, normalmente utilizaremos un `SELECT` dentro del procedimiento.

---

## Diferencia entre SELECT y OUT

Ambos pueden devolver información, pero tienen objetivos distintos.

### SELECT

Devuelve un conjunto de filas.

```sql
SELECT *
FROM Cliente;
```

---

### OUT

Devuelve un único valor.

```text
125
```

Es muy habitual combinar ambas técnicas dentro del mismo procedimiento.

---

## Buenas prácticas

* Utiliza `OUT` únicamente cuando sea necesario devolver un valor.
* Emplea nombres descriptivos para los parámetros.
* Inicializa las variables de sesión antes de llamar al procedimiento.
* Documenta claramente el significado del valor devuelto.

---

## Ideas clave

* Los parámetros `OUT` permiten devolver información desde un procedimiento.
* Se utilizan junto con variables de sesión.
* La instrucción `SELECT ... INTO` permite asignar valores a los parámetros.
* Un procedimiento puede combinar parámetros `IN` y `OUT`.
* Son ideales para devolver resultados únicos como contadores o importes.

