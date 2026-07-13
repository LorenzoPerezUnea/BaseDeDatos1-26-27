# HAVING

## Introducción

En la clase anterior aprendimos que la cláusula `WHERE` permite filtrar registros antes de que sean procesados.

Ahora surge una nueva necesidad.

Supongamos que queremos responder a la siguiente pregunta:

> ¿Qué ciudades tienen ​**más de 10 clientes**​?

No podemos escribir:

```sql
SELECT
    Ciudad,
    COUNT(*) AS TotalClientes
FROM Cliente
WHERE COUNT(*) > 10
GROUP BY Ciudad;
```

Esta consulta es incorrecta.

¿Por qué?

Porque `WHERE` se ejecuta **antes** de que exista el resultado de `COUNT()`.

Para resolver este problema SQL incorpora la cláusula ​**`HAVING`**​, cuya misión consiste en filtrar **grupos** en lugar de filas individuales.

---

## WHERE filtra filas, HAVING filtra grupos

La diferencia puede entenderse mediante el siguiente esquema.

```text
Tabla

        │

      WHERE
(Filtra registros)

        │

        ▼

GROUP BY

        │

(Funciones de agregación)

        │

        ▼

      HAVING
(Filtra grupos)

        │

        ▼

Resultado final
```

Esta diferencia es uno de los conceptos más importantes de SQL.

---

## Sintaxis

La estructura general es:

```sql
SELECT
    columnas,
    función_agregación
FROM Tabla
GROUP BY columna
HAVING condición;
```

Observa que `HAVING` siempre aparece **después** de `GROUP BY`.

---

## Primer ejemplo

Queremos mostrar únicamente aquellas ciudades que tengan más de cinco clientes.

```sql
SELECT
    Ciudad,
    COUNT(*) AS TotalClientes
FROM Cliente
GROUP BY Ciudad
HAVING COUNT(*) > 5;
```

Resultado:

| Ciudad    | TotalClientes |
| ----------- | --------------: |
| Santander |            35 |
| Bilbao    |            18 |
| Oviedo    |             9 |

Las ciudades con menos de cinco clientes ya no aparecen.

---

## Utilizando otras funciones

`HAVING` no está limitado a `COUNT()`.

También funciona con cualquier función de agregación.

Por ejemplo, mostrar únicamente las categorías cuyo precio medio sea superior a 500 €.

```sql
SELECT
    IdCategoria,
    AVG(Precio) AS PrecioMedio
FROM Producto
GROUP BY IdCategoria
HAVING AVG(Precio) > 500;
```

Solo aparecerán las categorías cuyo precio medio supere ese valor.

---

## Varias condiciones

También podemos combinar condiciones mediante operadores lógicos.

```sql
SELECT
    IdCategoria,
    COUNT(*) AS TotalProductos,
    AVG(Precio) AS PrecioMedio
FROM Producto
GROUP BY IdCategoria
HAVING
    COUNT(*) >= 5
    AND AVG(Precio) > 200;
```

Cada condición se evalúa sobre los valores agregados de cada grupo.

---

## Ordenando los grupos

Es muy habitual combinar `HAVING` con `ORDER BY`.

```sql
SELECT
    Ciudad,
    COUNT(*) AS TotalClientes
FROM Cliente
GROUP BY Ciudad
HAVING COUNT(*) > 5
ORDER BY TotalClientes DESC;
```

Primero se forman los grupos.

Después se eliminan los que no cumplen la condición.

Finalmente se ordenan los grupos restantes.

---

## Buenas prácticas

Antes de escribir una condición pregúntate:

> ¿Estoy filtrando registros individuales o grupos?

* Si filtras registros → `WHERE`.
* Si filtras grupos → `HAVING`.

Esta sencilla pregunta evita la mayoría de los errores relacionados con las agrupaciones.

---

## Ideas clave

* `HAVING` filtra grupos, no registros individuales.
* Siempre se utiliza después de `GROUP BY`.
* Permite utilizar funciones de agregación dentro de la condición.
* Puede combinarse con `ORDER BY`.
* Es imprescindible para construir consultas analíticas complejas.

