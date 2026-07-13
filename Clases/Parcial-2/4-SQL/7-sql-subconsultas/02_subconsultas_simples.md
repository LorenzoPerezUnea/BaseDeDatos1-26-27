# Subconsultas simples

## Introducción

Una vez comprendido por qué aparecen las subconsultas, comenzaremos con el caso más sencillo.

Una **subconsulta simple** es aquella que:

* se ejecuta primero;
* devuelve un único resultado;
* ese resultado es utilizado inmediatamente por la consulta principal.

Son las primeras subconsultas que normalmente aprende cualquier estudiante y constituyen la base para comprender las más avanzadas.

---

## ¿Cómo ejecuta MySQL una subconsulta?

Consideremos la siguiente consulta.

```sql
SELECT
    Nombre,
    Precio
FROM Producto
WHERE Precio >
(
    SELECT AVG(Precio)
    FROM Producto
);
```

Aunque parece una única consulta, internamente MySQL la ejecuta en dos etapas.

### Paso 1

Ejecuta la subconsulta.

```sql
SELECT AVG(Precio)
FROM Producto;
```

Supongamos que el resultado es:

```text
321.25
```

### Paso 2

Ese resultado sustituye a la subconsulta.

La consulta pasa a ser conceptualmente:

```sql
SELECT
    Nombre,
    Precio
FROM Producto
WHERE Precio > 321.25;
```

Finalmente se muestran únicamente los productos cuyo precio supera la media.

---

## Otro ejemplo

Queremos localizar el pedido más reciente.

```sql
SELECT *
FROM Pedido
WHERE Fecha =
(
    SELECT MAX(Fecha)
    FROM Pedido
);
```

Primero se calcula la fecha máxima.

Después se recuperan los pedidos correspondientes.

---

## Utilizando MIN()

También podemos localizar el producto más barato.

```sql
SELECT
    Nombre,
    Precio
FROM Producto
WHERE Precio =
(
    SELECT MIN(Precio)
    FROM Producto
);
```

Si varios productos tienen exactamente el mismo precio mínimo, todos aparecerán en el resultado.

---

## Utilizando MAX()

Del mismo modo:

```sql
SELECT
    Nombre,
    Precio
FROM Producto
WHERE Precio =
(
    SELECT MAX(Precio)
    FROM Producto
);
```

Obtendremos todos los productos cuyo precio sea el máximo.

---

## Subconsultas con COUNT()

También podemos comparar cantidades.

Por ejemplo, imaginemos una tabla de departamentos.

Queremos localizar aquellos departamentos cuyo número de empleados supera una determinada cantidad calculada previamente.

Aunque más adelante veremos ejemplos más completos, el mecanismo sigue siendo exactamente el mismo: una consulta calcula un valor y otra lo utiliza.

---

## ¿Qué devuelve una subconsulta simple?

Generalmente devuelve un único valor.

Por ejemplo:

```text
250

17

2026-05-12

95.3
```

Ese valor puede utilizarse prácticamente en cualquier comparación.

---

## Funciones habituales

Las funciones más utilizadas en este tipo de subconsultas son:

* `AVG()`
* `MIN()`
* `MAX()`
* `SUM()`
* `COUNT()`

Todas ellas producen un único resultado, por lo que son ideales para comenzar.

---

## Buenas prácticas

Siempre que una consulta necesite un único valor calculado por otra consulta:

* utiliza una subconsulta;
* evita ejecutar varias consultas manualmente;
* deja que sea MySQL quien gestione el proceso.

Esto hace que el código sea más robusto y mucho más fácil de mantener.

---

## Ideas clave

* Una subconsulta simple devuelve normalmente un único valor.
* MySQL ejecuta primero la subconsulta y después la consulta principal.
* Las funciones de agregación son las más utilizadas en este tipo de consultas.
* Constituyen la base para comprender todas las subconsultas más avanzadas.

