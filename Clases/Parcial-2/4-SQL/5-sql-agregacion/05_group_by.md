# GROUP BY

## Introducción

Hasta ahora todas las funciones de agregación se aplicaban sobre ​**toda la tabla**​.

Por ejemplo:

```sql
SELECT
    AVG(Precio)
FROM Producto;
```

Esta consulta devuelve un único precio medio para todos los productos.

Sin embargo, normalmente queremos responder preguntas más interesantes.

Por ejemplo:

* ¿Cuál es el precio medio de cada categoría?
* ¿Cuántos empleados hay por departamento?
* ¿Cuántos clientes viven en cada ciudad?
* ¿Cuál es el salario medio de cada oficina?

Para ello utilizaremos la cláusula ​**`GROUP BY`**​.

---

## ¿Qué hace GROUP BY?

`GROUP BY` divide los registros en grupos que comparten el mismo valor en una o varias columnas.

Después, las funciones de agregación se ejecutan ​**independientemente sobre cada grupo**​.

Visualmente:

```text
Tabla Producto

        │

GROUP BY Categoria

        │

        ▼

Portátiles
    ├── Producto A
    ├── Producto B

Monitores
    ├── Producto C
    ├── Producto D

Periféricos
    ├── Producto E
    ├── Producto F

        │

        ▼

COUNT()
AVG()
SUM()
MAX()
...
```

---

## Primer ejemplo

Supongamos que queremos conocer el número de productos de cada categoría.

```sql
SELECT
    IdCategoria,
    COUNT(*) AS TotalProductos
FROM Producto
GROUP BY IdCategoria;
```

Resultado:

| IdCategoria | TotalProductos |
| ------------: | ---------------: |
|           1 |             12 |
|           2 |              8 |
|           3 |             25 |

Ahora ya no obtenemos un único resultado, sino uno por cada grupo.

---

## Calculando medias por grupo

También podemos calcular el precio medio de cada categoría.

```sql
SELECT
    IdCategoria,
    AVG(Precio) AS PrecioMedio
FROM Producto
GROUP BY IdCategoria;
```

Resultado:

| IdCategoria | PrecioMedio |
| ------------: | ------------: |
|           1 |      825.50 |
|           2 |      245.75 |
|           3 |       48.20 |

Cada grupo produce su propio cálculo.

---

## Agrupando por texto

No es necesario agrupar únicamente por identificadores.

```sql
SELECT
    Ciudad,
    COUNT(*) AS TotalClientes
FROM Cliente
GROUP BY Ciudad;
```

Resultado:

| Ciudad    | TotalClientes |
| ----------- | --------------: |
| Santander |            35 |
| Bilbao    |            18 |
| Burgos    |            12 |

Esta consulta resulta muy útil para elaborar informes comerciales.

---

## Agrupar por varias columnas

Es posible crear grupos utilizando más de una columna.

```sql
SELECT
    Ciudad,
    Activo,
    COUNT(*) AS Total
FROM Cliente
GROUP BY
    Ciudad,
    Activo;
```

En este caso cada combinación de ciudad y estado (`Activo`) constituye un grupo diferente.

---

## Regla fundamental de GROUP BY

Existe una regla muy importante.

Cuando utilizamos `GROUP BY`, todas las columnas que aparecen en el `SELECT` deben cumplir una de estas dos condiciones:

* formar parte del `GROUP BY`;
* estar incluidas dentro de una función de agregación.

Por ejemplo, esta consulta es correcta.

```sql
SELECT
    IdCategoria,
    COUNT(*) AS Total
FROM Producto
GROUP BY IdCategoria;
```

Mientras que esta otra puede producir un error o resultados ambiguos.

```sql
SELECT
    Nombre,
    IdCategoria,
    COUNT(*)
FROM Producto
GROUP BY IdCategoria;
```

`Nombre` no pertenece al grupo ni está agregada.

---

## GROUP BY y ORDER BY

Con frecuencia ambas cláusulas aparecen juntas.

```sql
SELECT
    Ciudad,
    COUNT(*) AS TotalClientes
FROM Cliente
GROUP BY Ciudad
ORDER BY TotalClientes DESC;
```

Primero se forman los grupos.

Después se ordena el resultado obtenido.

---

## Ideas clave

* `GROUP BY` crea grupos de registros.
* Las funciones de agregación se calculan para cada grupo.
* Puede utilizarse con una o varias columnas.
* Las columnas del `SELECT` deben estar agrupadas o agregadas.
* `GROUP BY` constituye la base de la mayoría de informes analíticos en SQL.

