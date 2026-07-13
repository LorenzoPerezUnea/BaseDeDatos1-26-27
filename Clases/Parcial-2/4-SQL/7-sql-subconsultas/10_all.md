# ALL

## Introducción

En el apartado anterior estudiamos el operador `ANY`, cuya condición se cumple cuando la comparación es verdadera para **al menos uno** de los valores devueltos por la subconsulta.

Ahora estudiaremos el operador contrario:

​**`ALL`**​.

Mientras que `ANY` significa:

> "al menos uno"

`ALL` significa:

> **"todos"**

La condición únicamente será verdadera cuando la comparación se cumpla **para todos los valores** devueltos por la subconsulta.

Es un operador menos frecuente, pero muy útil para determinados problemas de análisis de datos.

---

## Sintaxis

```sql
SELECT
    columnas
FROM Tabla
WHERE valor > ALL
(
    subconsulta
);
```

La subconsulta devuelve varias filas y el operador compara el valor con todas ellas.

---

## Primer ejemplo

Supongamos que la categoría **Periféricos** contiene estos precios:

```text
25
45
60
90
```

Queremos obtener los productos cuyo precio sea superior a **todos** los precios de esa categoría.

```sql
SELECT
    Nombre,
    Precio
FROM Producto
WHERE Precio > ALL
(
    SELECT Precio
    FROM Producto
    WHERE IdCategoria = 1
);
```

---

## ¿Cómo interpreta MySQL esta consulta?

Conceptualmente equivale a comprobar:

```text
Precio > 25

Y

Precio > 45

Y

Precio > 60

Y

Precio > 90
```

Observa la diferencia respecto a `ANY`.

Ahora **todas** las comparaciones deben ser verdaderas.

---

## Ejemplo

Si un producto cuesta:

```text
120 €
```

Comparaciones:

```text
120 > 25   ✔

120 > 45   ✔

120 > 60   ✔

120 > 90   ✔
```

Como todas son verdaderas, el producto aparece en el resultado.

Si costara 70 €:

```text
70 > 25   ✔

70 > 45   ✔

70 > 60   ✔

70 > 90   ✘
```

La condición ya no se cumple.

---

## Relación con MAX()

Cuando utilizamos:

```sql
> ALL
```

el comportamiento es equivalente a comparar con el valor máximo del conjunto.

Es decir:

```sql
Precio > ALL (...)
```

puede entenderse como:

```sql
Precio >
(
    SELECT MAX(Precio)
    ...
)
```

Esta equivalencia resulta muy útil para comprender el funcionamiento del operador.

---

## Otro ejemplo

Mostrar los empleados cuyo salario sea superior al de todos los empleados del departamento de Marketing.

```sql
SELECT
    Nombre,
    Salario
FROM Empleado
WHERE Salario > ALL
(
    SELECT Salario
    FROM Empleado
    WHERE Departamento = 'Marketing'
);
```

Solo aparecerán aquellos empleados cuyo salario supere incluso al mejor pagado de Marketing.

---

## ¿Cuándo utilizar ALL?

Aunque muchas consultas pueden escribirse utilizando `MAX()` o `MIN()`, `ALL` resulta especialmente útil cuando queremos expresar claramente que una comparación debe cumplirse respecto a todos los valores de un conjunto.

Su uso hace que la intención de la consulta sea muy explícita.

---

## Comparación entre ANY y ALL

| Operador    | Significado      | Equivalencia conceptual |
| ------------- | ------------------ | ------------------------- |
| `> ANY` | Mayor que alguno | Mayor que el mínimo    |
| `< ANY` | Menor que alguno | Menor que el máximo    |
| `> ALL` | Mayor que todos  | Mayor que el máximo    |
| `< ALL` | Menor que todos  | Menor que el mínimo    |

Estas equivalencias ayudan a interpretar rápidamente el comportamiento de ambos operadores.

---

## Ideas clave

* `ALL` exige que la condición sea verdadera para todos los valores devueltos por la subconsulta.
* Se utiliza con subconsultas que devuelven múltiples filas.
* Con el operador `>` puede interpretarse como una comparación con el valor máximo del conjunto.
* Es menos frecuente que `EXISTS` o `IN`, pero forma parte del SQL estándar y conviene conocerlo.

