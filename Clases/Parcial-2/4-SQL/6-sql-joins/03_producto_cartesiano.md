# Producto cartesiano

## Introducción

Antes de estudiar los distintos tipos de `JOIN`, es imprescindible comprender un concepto matemático del que derivan todas las uniones entre tablas:

​**el producto cartesiano**​.

Aunque en la práctica rara vez querremos obtener un producto cartesiano completo, entender su funcionamiento permite comprender qué hace realmente un `JOIN`.

---

## ¿Qué es un producto cartesiano?

El producto cartesiano consiste en combinar ​**cada fila de una tabla con todas las filas de la otra tabla**​.

Si una tabla tiene:

* 3 registros

y otra tiene:

* 4 registros

el resultado contendrá:

```text
3 × 4 = 12 filas
```

Cada registro de la primera tabla aparece combinado con todos los registros de la segunda.

---

## Ejemplo sencillo

Supongamos las siguientes tablas.

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

El producto cartesiano produce:

| Color | Talla |
| ------- | ------- |
| Rojo  | S     |
| Rojo  | M     |
| Rojo  | L     |
| Azul  | S     |
| Azul  | M     |
| Azul  | L     |

Cada color aparece combinado con todas las tallas posibles.

---

## En SQL

Podemos obtener este resultado utilizando `CROSS JOIN`, aunque también puede producirse accidentalmente si olvidamos la condición del `JOIN`.

```sql
SELECT
    *
FROM Color
CROSS JOIN Talla;
```

Resultado:

```text
2 × 3 = 6 filas
```

---

## ¿Por qué es importante?

Porque todos los `JOIN` pueden entenderse conceptualmente como un proceso en dos etapas:

1. Se genera el producto cartesiano.
2. Se eliminan las combinaciones que no cumplen la condición del `JOIN`.

Por ejemplo:

```sql
SELECT
    Cliente.Nombre,
    Pedido.IdPedido
FROM Cliente
INNER JOIN Pedido
ON Cliente.IdCliente = Pedido.IdCliente;
```

SQL no muestra todas las combinaciones posibles.

Únicamente conserva aquellas donde el identificador del cliente coincide con el del pedido.

---

## El peligro de olvidar la condición

Uno de los errores más graves consiste en escribir una consulta que combine varias tablas sin indicar cómo deben relacionarse.

Por ejemplo:

```sql
SELECT
    *
FROM Cliente
JOIN Pedido;
```

o, en versiones antiguas de SQL:

```sql
SELECT
    *
FROM Cliente,
     Pedido;
```

Si no existe una condición adecuada, el resultado puede contener millones de filas innecesarias.

Supongamos:

* 2.000 clientes.
* 50.000 pedidos.

El producto cartesiano generaría:

```text
2.000 × 50.000

=

100.000.000 filas
```

Aunque muchas de ellas no tengan ningún sentido.

Este tipo de errores puede ralentizar gravemente una base de datos.

---

## ¿Cuándo se utiliza realmente?

Aunque normalmente intentamos evitar el producto cartesiano, existen casos donde resulta útil.

Por ejemplo:

* generar todas las combinaciones posibles de colores y tallas;
* crear calendarios;
* generar horarios;
* construir matrices de datos;
* realizar pruebas automáticas.

En estos casos se utiliza explícitamente `CROSS JOIN`, que estudiaremos más adelante.

---

## Ideas clave

* El producto cartesiano combina todas las filas de una tabla con todas las filas de la otra.
* Si una tabla tiene **m** filas y otra ​**n**​, el resultado tendrá **m × n** filas.
* Conceptualmente, los `JOIN` parten del producto cartesiano y después aplican una condición para conservar únicamente las combinaciones válidas.
* Olvidar la condición de unión puede generar resultados enormes y afectar gravemente al rendimiento.
* Comprender el producto cartesiano facilita entender el funcionamiento interno de todos los tipos de `JOIN`.

