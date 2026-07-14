# Bucles WHILE

## Introducción

Hasta este momento, todos nuestros procedimientos ejecutaban las instrucciones una única vez.

Sin embargo, existen situaciones en las que necesitamos repetir una operación varias veces.

Por ejemplo:

* recorrer una secuencia de números;
* procesar varios registros;
* generar datos de prueba;
* realizar cálculos iterativos;
* repetir una acción hasta que se cumpla una condición.

Para ello MySQL incorpora estructuras repetitivas, siendo la más utilizada ​**WHILE**​.

---

## ¿Qué es un bucle?

Un **bucle** es una estructura que repite un bloque de instrucciones mientras una condición sea verdadera.

Su funcionamiento puede representarse así:

```text
Comprobar condición

↓

¿Se cumple?

↓

Sí ──────────────┐
│                │
Ejecutar bloque  │
│                │
└────────────────┘

No

↓

Finalizar
```

Cada repetición recibe el nombre de ​**iteración**​.

---

## Sintaxis

La estructura general es:

```sql
WHILE condicion DO

    instrucciones;

END WHILE;
```

Mientras la condición sea verdadera, MySQL seguirá ejecutando el bloque.

---

## Primer ejemplo

Mostrar los números del 1 al 5.

```sql
DELIMITER $$

CREATE PROCEDURE ContarHastaCinco()

BEGIN

    DECLARE Contador INT DEFAULT 1;

    WHILE Contador <= 5 DO

        SELECT Contador;

        SET Contador = Contador + 1;

    END WHILE;

END $$

DELIMITER ;
```

Ejecución:

```sql
CALL ContarHastaCinco();
```

Resultado:

```text
1
2
3
4
5
```

---

## La importancia del incremento

Observa esta línea:

```sql
SET Contador = Contador + 1;
```

Es fundamental.

Si olvidamos actualizar el contador:

```sql
WHILE Contador <= 5 DO

    SELECT Contador;

END WHILE;
```

la condición nunca dejará de cumplirse.

Obtendremos un ​**bucle infinito**​.

Este es uno de los errores más habituales cuando se empieza a programar.

---

## Ejemplo práctico

Supongamos que queremos generar cinco productos de prueba.

```sql
DELIMITER $$

CREATE PROCEDURE GenerarProductos()

BEGIN

    DECLARE i INT DEFAULT 1;

    WHILE i <= 5 DO

        INSERT INTO Producto
        (Nombre, Precio)

        VALUES

        (CONCAT('Producto ', i), i * 100);

        SET i = i + 1;

    END WHILE;

END $$

DELIMITER ;
```

Después de ejecutarlo:

```sql
CALL GenerarProductos();
```

La tabla contendrá cinco nuevos registros.

---

## Uso con variables

Los bucles suelen combinarse con variables.

```sql
DECLARE Total INT DEFAULT 0;

DECLARE i INT DEFAULT 1;

WHILE i <= 10 DO

    SET Total = Total + i;

    SET i = i + 1;

END WHILE;

SELECT Total;
```

Resultado:

```text
55
```

Se ha calculado la suma de los diez primeros números naturales.

---

## ¿Cuándo utilizar WHILE?

Es recomendable cuando conocemos claramente la condición de finalización.

Por ejemplo:

* repetir N veces;
* recorrer una secuencia;
* generar registros;
* realizar cálculos repetitivos.

Cuando el objetivo es recorrer filas de una consulta, normalmente se utilizan ​**cursores**​, que veremos en el siguiente apartado.

---

## Buenas prácticas

* Inicializa correctamente las variables.
* Asegúrate de que la condición terminará cumpliéndose.
* Evita bucles innecesariamente largos.
* Mantén el código del bucle sencillo.
* Comprueba siempre que el contador se actualiza.

---

## Ideas clave

* `WHILE` permite repetir instrucciones.
* La repetición continúa mientras la condición sea verdadera.
* Es imprescindible actualizar la condición para evitar bucles infinitos.
* Se utiliza habitualmente junto con variables.
* Es muy útil para automatizar tareas repetitivas.

