# GROUP BY vs WHERE

## Introducción

Uno de los errores más frecuentes entre los estudiantes consiste en confundir las cláusulas `WHERE` y `HAVING`.

Ambas permiten establecer condiciones, pero actúan en momentos completamente distintos del proceso de ejecución de una consulta.

Comprender esta diferencia es esencial para escribir consultas correctas.

---

## Comparación general

| WHERE                                               | HAVING                                      |
| ----------------------------------------------------- | --------------------------------------------- |
| Filtra filas individuales                           | Filtra grupos completos                     |
| Se ejecuta antes de`GROUP BY`                   | Se ejecuta después de`GROUP BY`        |
| No puede utilizar funciones de agregación          | Sí puede utilizar funciones de agregación |
| Reduce el número de registros que serán agrupados | Reduce el número de grupos obtenidos       |

En la práctica, ambas cláusulas suelen aparecer juntas.

---

## Ejemplo utilizando WHERE

Queremos analizar únicamente los productos activos.

```sql
SELECT
    IdCategoria,
    COUNT(*) AS TotalProductos
FROM Producto
WHERE Activo = TRUE
GROUP BY IdCategoria;
```

Proceso:

1. Se eliminan los productos inactivos.
2. Se crean los grupos.
3. Se cuenta el número de productos de cada grupo.

---

## Ejemplo utilizando HAVING

Ahora queremos mostrar únicamente las categorías con más de cinco productos.

```sql
SELECT
    IdCategoria,
    COUNT(*) AS TotalProductos
FROM Producto
GROUP BY IdCategoria
HAVING COUNT(*) > 5;
```

Proceso:

1. Se forman todos los grupos.
2. Se calcula `COUNT()`.
3. Se eliminan los grupos cuyo total sea inferior o igual a cinco.

---

## Combinando WHERE y HAVING

En aplicaciones reales es muy habitual utilizar ambas cláusulas simultáneamente.

```sql
SELECT
    IdCategoria,
    AVG(Precio) AS PrecioMedio
FROM Producto
WHERE Activo = TRUE
GROUP BY IdCategoria
HAVING AVG(Precio) > 200
ORDER BY PrecioMedio DESC;
```

Orden lógico de ejecución:

1. `FROM`
2. `WHERE`
3. `GROUP BY`
4. Funciones de agregación
5. `HAVING`
6. `SELECT`
7. `ORDER BY`

Este ejemplo resume prácticamente todo lo aprendido en las dos últimas clases.

---

## ¿Cuándo utilizar cada una?

Utiliza `WHERE` cuando la condición haga referencia a una fila concreta.

Ejemplos:

* Precio > 100
* Ciudad = 'Santander'
* Activo = TRUE

Utiliza `HAVING` cuando la condición haga referencia al resultado de una agregación.

Ejemplos:

* COUNT(\*) > 10
* AVG(Precio) > 500
* SUM(Importe) > 10000

---

## Error típico

Muchos estudiantes escriben:

```sql
SELECT
    Ciudad,
    COUNT(*)
FROM Cliente
WHERE COUNT(*) > 5
GROUP BY Ciudad;
```

Esta consulta es incorrecta porque `COUNT()` todavía no existe cuando se ejecuta `WHERE`.

La versión correcta es:

```sql
SELECT
    Ciudad,
    COUNT(*) AS TotalClientes
FROM Cliente
GROUP BY Ciudad
HAVING COUNT(*) > 5;
```

---

## Buenas prácticas

Una regla sencilla consiste en recordar:

* **WHERE responde a la pregunta "¿qué filas participan?"**
* **HAVING responde a la pregunta "¿qué grupos se muestran?"**

Si aplicas esta idea, distinguir ambas cláusulas resultará mucho más sencillo.

---

## Ideas clave

* `WHERE` filtra registros antes de agrupar.
* `HAVING` filtra grupos después de agrupar.
* Las funciones de agregación solo pueden utilizarse en `HAVING` (o en el `SELECT`).
* Ambas cláusulas son complementarias y suelen utilizarse juntas.
* Comprender su diferencia es fundamental para desarrollar consultas SQL correctas y eficientes.

