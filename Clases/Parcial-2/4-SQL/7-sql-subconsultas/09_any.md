# ANY

## Introducción

Hasta ahora nuestras comparaciones utilizaban operadores sencillos como:

```sql
=
>
<
>=
<=
<>
```

Todos ellos comparaban un valor con otro valor.

Pero ¿qué ocurre cuando una subconsulta devuelve ​**varios valores**​?

Por ejemplo:

```sql
SELECT Precio
FROM Producto
WHERE IdCategoria = 3;
```

Esta consulta puede devolver:

```text
120
250
430
690
```

Ya no podemos escribir:

```sql
WHERE Precio > (subconsulta)
```

porque la subconsulta devuelve más de una fila.

Para resolver este problema aparece el operador ​**`ANY`**​.

---

## ¿Qué significa ANY?

`ANY` significa literalmente:

> **"al menos uno de los valores devueltos".**

La condición será verdadera si la comparación se cumple con **alguno** de los resultados de la subconsulta.

---

## Sintaxis

```sql
SELECT ...
FROM ...
WHERE valor > ANY
(
    subconsulta
);
```

La subconsulta devuelve varios valores.

El operador compara el valor con todos ellos.

---

## Primer ejemplo

Supongamos los siguientes precios de la categoría "Monitores":

```text
250
320
450
600
```

Consulta:

```sql
SELECT
    Nombre,
    Precio
FROM Producto
WHERE Precio > ANY
(
    SELECT Precio
    FROM Producto
    WHERE IdCategoria = 2
);
```

---

## ¿Cómo se interpreta?

MySQL evalúa la condición de esta forma:

```text
Precio > 250

O

Precio > 320

O

Precio > 450

O

Precio > 600
```

Basta con que una de ellas sea verdadera.

---

## Ejemplo

Si un producto cuesta:

```text
500 €
```

Comparaciones:

```text
500 > 250   ✔

500 > 320   ✔

500 > 450   ✔

500 > 600   ✘
```

Como al menos una comparación es verdadera, el producto aparece en el resultado.

---

## Relación con MIN()

Cuando utilizamos el operador `>`:

```sql
> ANY
```

el comportamiento es equivalente a comparar con el valor mínimo del conjunto.

Por ejemplo:

```sql
Precio > ANY (...)
```

es conceptualmente similar a:

```sql
Precio >
(
    SELECT MIN(Precio)
    ...
)
```

Aunque el optimizador puede tratarlas de forma diferente, esta equivalencia ayuda mucho a comprender el funcionamiento del operador.

---

## Casos de uso

`ANY` suele utilizarse cuando queremos comparar un valor con un conjunto de resultados y basta con superar uno de ellos.

Por ejemplo:

* productos más caros que alguno de otra categoría;
* empleados con mayor salario que algún empleado de otro departamento;
* pedidos superiores a alguna compra realizada el mes anterior.

Aunque no es un operador tan frecuente como `EXISTS`, forma parte del estándar SQL y conviene conocerlo.

---

## Ideas clave

* `ANY` compara un valor con todos los resultados de una subconsulta.
* La condición se cumple si al menos una comparación es verdadera.
* Se utiliza con subconsultas que devuelven múltiples filas.
* Con el operador `>` puede entenderse como una comparación con el valor mínimo del conjunto.
* Es un operador útil para determinados problemas de comparación múltiple.

