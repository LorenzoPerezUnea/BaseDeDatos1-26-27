# CROSS JOIN

## Introducción

En apartados anteriores estudiamos el ​**producto cartesiano**​, explicando que consistía en combinar cada fila de una tabla con todas las filas de otra.

Ahora veremos la operación SQL que realiza exactamente ese comportamiento de forma explícita:

​**`CROSS JOIN`**​.

Aunque no es uno de los JOIN más utilizados en aplicaciones de gestión, resulta muy útil en determinados escenarios y ayuda a comprender el funcionamiento interno de los demás tipos de JOIN.

---

## ¿Qué hace CROSS JOIN?

`CROSS JOIN` genera el **producto cartesiano** de dos tablas.

Es decir:

* cada fila de la primera tabla se combina con todas las filas de la segunda;
* no existe ninguna condición de unión;
* todas las combinaciones posibles forman parte del resultado.

Si una tabla tiene **m** filas y la otra ​**n**​, el resultado tendrá:

```text
m × n filas
```

---

## Ejemplo sencillo

Supongamos dos tablas.

### Color

| Color |
| ------- |
| Rojo  |
| Azul  |

### Talla

| Talla |
| ------- |
| S     |
| M     |
| L     |

Consulta:

```sql
SELECT
    Color.Color,
    Talla.Talla
FROM Color
CROSS JOIN Talla;
```

Resultado:

| Color | Talla |
| ------- | ------- |
| Rojo  | S     |
| Rojo  | M     |
| Rojo  | L     |
| Azul  | S     |
| Azul  | M     |
| Azul  | L     |

Cada color aparece combinado con todas las tallas.

---

## ¿Por qué no necesita ON?

A diferencia de `INNER JOIN`, `LEFT JOIN` o `RIGHT JOIN`, `CROSS JOIN`​**no compara columnas**​.

Por tanto, no existe una condición de unión.

La sintaxis correcta es:

```sql
SELECT
    *
FROM TablaA
CROSS JOIN TablaB;
```

No debe añadirse una cláusula `ON`.

---

## Aplicaciones reales

Aunque pueda parecer una operación poco frecuente, tiene aplicaciones muy interesantes.

### Generación de variantes de productos

Una tienda de ropa puede generar automáticamente todas las combinaciones entre:

* colores;
* tallas;
* materiales.

Por ejemplo:

| Color | Talla | Material |
| ------- | ------- | ---------- |
| Azul  | M     | Algodón |
| Azul  | M     | Lana     |
| Negro | L     | Algodón |
| ...   | ...   | ...      |

---

### Generación de calendarios

Puede utilizarse para combinar:

* días;
* horas;
* aulas.

Generando automáticamente todos los posibles horarios.

---

### Datos de prueba

En desarrollo es habitual utilizar `CROSS JOIN` para generar rápidamente miles de registros de prueba combinando tablas pequeñas.

---

## Riesgos

El principal inconveniente es el enorme crecimiento del número de filas.

Por ejemplo:

| Tabla A | Tabla B |   Resultado |
| --------: | --------: | ------------: |
|     100 |      50 |       5.000 |
|   1.000 |     500 |     500.000 |
|  10.000 |  20.000 | 200.000.000 |

Como puede observarse, el crecimiento es multiplicativo.

Por ello debe utilizarse con cuidado.

---

## Diferencia respecto a olvidar el ON

Una consulta escrita incorrectamente puede generar accidentalmente un producto cartesiano.

Por ejemplo:

```sql
SELECT
    *
FROM Cliente,
     Pedido;
```

En SQL moderno siempre es preferible utilizar la sintaxis explícita de `JOIN`, ya que resulta mucho más clara y reduce el riesgo de cometer errores.

---

## Buenas prácticas

Utiliza `CROSS JOIN` únicamente cuando realmente necesites todas las combinaciones posibles.

En cualquier otro caso, probablemente deberías utilizar `INNER JOIN`, `LEFT JOIN` o `RIGHT JOIN`.

---

## Ideas clave

* `CROSS JOIN` genera el producto cartesiano de dos tablas.
* No utiliza una cláusula `ON`.
* El número de filas resultante es el producto del tamaño de ambas tablas.
* Resulta útil para generar combinaciones, calendarios y datos de prueba.
* Debe utilizarse con precaución debido al rápido crecimiento del número de registros.

