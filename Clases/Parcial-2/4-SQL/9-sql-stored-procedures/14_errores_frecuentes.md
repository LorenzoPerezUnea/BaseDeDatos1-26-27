# Errores frecuentes

## Introducción

Los procedimientos almacenados incorporan conceptos propios de la programación además de SQL.

Por ello, los errores más habituales no solo están relacionados con la sintaxis, sino también con la lógica del algoritmo.

Conocer estos problemas ayuda a desarrollar procedimientos más robustos y fáciles de mantener.

---

## Error 1. Olvidar cambiar el delimitador

Uno de los errores más comunes al comenzar.

Incorrecto:

```sql
CREATE PROCEDURE Ejemplo()

BEGIN

    SELECT * FROM Cliente;

END;
```

MySQL interpretará el primer `;` como el final de la instrucción.

Correcto:

```sql
DELIMITER $$

...

DELIMITER ;
```

---

## Error 2. No utilizar `CALL`

Muchos estudiantes intentan ejecutar un procedimiento mediante:

```sql
SELECT RegistrarPedido();
```

Esto es incorrecto.

La forma adecuada es:

```sql
CALL RegistrarPedido();
```

---

## Error 3. No declarar las variables al principio

Las instrucciones `DECLARE` deben situarse al comienzo del bloque `BEGIN...END`.

Incorrecto:

```sql
SELECT *

FROM Cliente;

DECLARE Total INT;
```

Correcto:

```sql
DECLARE Total INT;

SELECT *

FROM Cliente;
```

---

## Error 4. Crear bucles infinitos

Un error muy frecuente consiste en olvidar actualizar el contador.

```sql
WHILE Contador < 10 DO

    SELECT Contador;

END WHILE;
```

Como `Contador` nunca cambia, el bucle no termina.

Debe incluirse:

```sql
SET Contador = Contador + 1;
```

---

## Error 5. No validar parámetros

Un procedimiento que recibe una cantidad negativa o un identificador inexistente puede producir resultados inesperados.

Siempre conviene comprobar los datos antes de realizar modificaciones sobre la base de datos.

---

## Error 6. Pensar que los procedimientos sustituyen a la aplicación

Los procedimientos son una herramienta muy útil, pero no deben contener toda la lógica del sistema.

En aplicaciones modernas, lo habitual es repartir las responsabilidades entre:

* la aplicación;
* la base de datos.

Cada componente debe realizar las tareas para las que está mejor preparado.

---

## Error 7. Utilizar cursores innecesariamente

Muchos problemas que pueden resolverse mediante:

```sql
UPDATE

JOIN

GROUP BY
```

se implementan incorrectamente mediante cursores.

Esto suele producir un rendimiento inferior.

Los cursores deben reservarse para casos donde realmente sean necesarios.

---

## Error 8. No documentar los procedimientos

Después de varios meses resulta difícil recordar:

* qué hace un procedimiento;
* qué parámetros recibe;
* qué tablas modifica.

Una breve documentación evita muchas horas de mantenimiento.

---

## Recomendaciones

Antes de ejecutar un procedimiento revisa:

* delimitadores;
* parámetros;
* variables;
* condiciones;
* bucles;
* mensajes de error.

Una revisión rápida suele detectar la mayoría de los problemas antes de poner el procedimiento en producción.

---

## Ideas clave

* Utiliza siempre `DELIMITER` al crear procedimientos.
* Ejecútalos mediante `CALL`.
* Declara las variables al comienzo del bloque.
* Evita bucles infinitos.
* Valida los parámetros de entrada.
* No utilices cursores cuando una consulta basada en conjuntos sea suficiente.
* Documenta el propósito y funcionamiento de cada procedimiento.

