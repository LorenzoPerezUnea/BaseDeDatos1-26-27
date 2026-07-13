# SUM, AVG, MIN y MAX

## Introducción

Además de contar registros mediante `COUNT()`, SQL incorpora otras funciones de agregación que permiten realizar operaciones matemáticas sobre un conjunto de datos.

Las cuatro funciones más utilizadas son:

* `SUM()`
* `AVG()`
* `MIN()`
* `MAX()`

Estas funciones aparecen continuamente en informes financieros, sistemas de inventario, aplicaciones de recursos humanos y cuadros de mando empresariales.

Con ellas podremos responder preguntas como:

* ¿Cuál es el valor total del inventario?
* ¿Cuál es el precio medio de los productos?
* ¿Cuál es el salario más alto de la empresa?
* ¿Cuál es el producto más barato?

---

## SUM()

La función `SUM()` calcula la suma de todos los valores de una columna numérica.

Supongamos la siguiente tabla.

| Producto  | Precio |
| ----------- | -------: |
| Ratón    |     25 |
| SSD       |    120 |
| Monitor   |    280 |
| Portátil |    950 |

La consulta:

```sql
SELECT
    SUM(Precio) AS TotalInventario
FROM Producto;
```

Resultado:

| TotalInventario |
| ----------------: |
|            1375 |

`SUM()` únicamente puede utilizarse sobre columnas numéricas.

---

## AVG()

`AVG()` calcula la media aritmética.

```sql
SELECT
    AVG(Precio) AS PrecioMedio
FROM Producto;
```

Resultado:

| PrecioMedio |
| ------------: |
|      343.75 |

Internamente, MySQL suma todos los valores y los divide entre el número de registros considerados.

Los valores `NULL` no participan en el cálculo.

---

## MIN()

`MIN()` devuelve el menor valor existente.

```sql
SELECT
    MIN(Precio) AS ProductoMasBarato
FROM Producto;
```

Resultado:

| ProductoMasBarato |
| ------------------: |
|                25 |

También puede utilizarse sobre fechas.

```sql
SELECT
    MIN(FechaRegistro) AS PrimerCliente
FROM Cliente;
```

En este caso obtendríamos la fecha del cliente registrado hace más tiempo.

---

## MAX()

`MAX()` realiza la operación opuesta.

```sql
SELECT
    MAX(Precio) AS ProductoMasCaro
FROM Producto;
```

Resultado:

| ProductoMasCaro |
| ----------------: |
|             950 |

Sobre fechas devuelve la fecha más reciente.

```sql
SELECT
    MAX(FechaRegistro) AS UltimoRegistro
FROM Cliente;
```

---

## Utilizando varias funciones simultáneamente

Es habitual calcular varios indicadores en una única consulta.

```sql
SELECT
    COUNT(*) AS TotalProductos,
    SUM(Precio) AS ValorInventario,
    AVG(Precio) AS PrecioMedio,
    MIN(Precio) AS PrecioMinimo,
    MAX(Precio) AS PrecioMaximo
FROM Producto;
```

Resultado:

| TotalProductos | ValorInventario | PrecioMedio | PrecioMinimo | PrecioMaximo |
| ---------------: | ----------------: | ------------: | -------------: | -------------: |
|              4 |            1375 |      343.75 |           25 |          950 |

Esta técnica es muy utilizada para generar paneles de indicadores.

---

## Combinando con WHERE

Las funciones de agregación pueden calcularse únicamente sobre un subconjunto de registros.

```sql
SELECT
    AVG(Precio) AS PrecioMedio
FROM Producto
WHERE Activo = TRUE;
```

Primero se filtran los productos activos y después se calcula la media.

Esto permite obtener estadísticas muy precisas.

---

## Buenas prácticas

Cuando utilices funciones de agregación:

* utiliza alias descriptivos;
* asegúrate de que la columna es numérica cuando corresponda;
* filtra previamente con `WHERE` si es necesario;
* recuerda que los valores `NULL` suelen ignorarse.

---

## Ideas clave

* `SUM()` calcula el total de una columna.
* `AVG()` obtiene la media aritmética.
* `MIN()` devuelve el menor valor.
* `MAX()` devuelve el mayor valor.
* Varias funciones pueden combinarse en una misma consulta.
* Son la base de la mayoría de informes estadísticos.

