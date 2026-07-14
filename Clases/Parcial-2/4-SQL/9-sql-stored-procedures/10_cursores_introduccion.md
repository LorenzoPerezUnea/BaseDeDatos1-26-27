# Cursores: introducción

## Introducción

Hasta ahora nuestras consultas SQL trabajaban con conjuntos completos de registros.

Por ejemplo:

```sql
SELECT *
FROM Cliente;
```

El resultado contiene todas las filas al mismo tiempo.

Sin embargo, en ocasiones necesitamos procesar los registros ​**uno por uno**​.

Por ejemplo:

* enviar un correo a cada cliente;
* recalcular el saldo de cada cuenta;
* actualizar registros siguiendo un orden determinado;
* generar un informe personalizado para cada empleado.

Para estas situaciones MySQL proporciona los ​**cursores (CURSOR)**​.

---

## ¿Qué es un cursor?

Un cursor es un mecanismo que permite recorrer el resultado de una consulta fila a fila.

Su funcionamiento puede representarse así:

```text
Consulta

↓

Fila 1

↓

Fila 2

↓

Fila 3

↓

...

↓

Última fila
```

En lugar de trabajar con todo el conjunto simultáneamente, podemos analizar cada registro individualmente.

---

## ¿Por qué existen?

SQL está diseñado para trabajar con conjuntos de datos.

Por ello, siempre que sea posible, debemos utilizar consultas normales.

Los cursores solo deben emplearse cuando realmente sea necesario realizar un procesamiento secuencial.

En bases de datos grandes, una consulta basada en conjuntos suele ser mucho más eficiente que recorrer millones de filas una a una.

---

## Funcionamiento general

El uso de un cursor suele seguir estos pasos:

1. Declarar el cursor.
2. Declarar una condición de fin.
3. Abrir el cursor.
4. Leer una fila.
5. Procesar la información.
6. Repetir hasta llegar al final.
7. Cerrar el cursor.

Es un proceso similar al recorrido de un archivo en programación.

---

## Declarar un cursor

Ejemplo:

```sql
DECLARE CursorClientes CURSOR FOR

SELECT
    IdCliente,
    Nombre
FROM Cliente;
```

El cursor queda asociado a una consulta.

Todavía no se ha ejecutado.

---

## Abrir el cursor

```sql
OPEN CursorClientes;
```

En este momento MySQL prepara el recorrido del conjunto de resultados.

---

## Leer registros

Cada lectura obtiene una única fila.

```sql
FETCH CursorClientes

INTO vIdCliente,
     vNombre;
```

Los datos recuperados se almacenan en variables locales.

---

## Cerrar el cursor

Una vez terminado el recorrido:

```sql
CLOSE CursorClientes;
```

Cerrar el cursor libera los recursos utilizados por el servidor.

---

## ¿Veremos cursores en profundidad?

No en esta asignatura.

El objetivo es que el estudiante comprenda:

* qué son;
* cuándo se utilizan;
* cómo funcionan de forma general.

En cursos avanzados de administración de bases de datos o programación SQL se estudian técnicas más complejas relacionadas con cursores, manejadores de eventos y optimización.

---

## Buenas prácticas

* Utiliza cursores únicamente cuando no exista una alternativa basada en consultas.
* Cierra siempre el cursor al finalizar.
* Mantén el procesamiento de cada fila lo más simple posible.
* Evita recorrer grandes volúmenes de datos si puede resolverse mediante `UPDATE`, `JOIN` o funciones de agregación.

---

## Ideas clave

* Un cursor permite recorrer una consulta fila a fila.
* Su uso es excepcional; SQL está pensado para trabajar con conjuntos.
* Todo cursor debe declararse, abrirse, utilizarse y cerrarse correctamente.
* Los cursores suelen combinarse con bucles y variables.
* Constituyen una herramienta útil para determinadas tareas procedimentales, pero deben utilizarse con criterio.

