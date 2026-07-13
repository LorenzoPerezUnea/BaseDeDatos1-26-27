# Subconsultas en FROM

## Introducción

Hasta ahora hemos utilizado subconsultas para obtener un valor que posteriormente era utilizado en la cláusula `WHERE`.

Sin embargo, existe otra posibilidad muy interesante:

​**utilizar una subconsulta como si fuera una tabla temporal**​.

En este caso, la subconsulta aparece dentro de la cláusula `FROM` y su resultado puede consultarse exactamente igual que cualquier otra tabla.

Esta técnica resulta muy útil cuando necesitamos realizar una consulta sobre el resultado de otra consulta.

---

## La idea fundamental

Supongamos que primero queremos calcular las ventas totales realizadas por cada cliente.

Después queremos trabajar únicamente con ese resultado.

Visualmente:

```text
Tabla Pedido

        │

        ▼

Subconsulta

(Totales por cliente)

        │

        ▼

Consulta principal
```

La consulta principal ya no trabaja directamente sobre `Pedido`, sino sobre el resultado generado por la subconsulta.

---

## Sintaxis general

```sql
SELECT
    columnas
FROM
(
    SELECT ...
    FROM ...
) AS NombreTemporal;
```

Observa un detalle importante:

> **Toda subconsulta situada en FROM debe tener un alias.**

Ese alias actúa como el nombre de la tabla temporal.

---

## Primer ejemplo

Queremos calcular el gasto realizado por cada cliente.

```sql
SELECT
    t.IdCliente,
    t.TotalGastado
FROM
(
    SELECT
        IdCliente,
        SUM(Total) AS TotalGastado
    FROM Pedido
    GROUP BY IdCliente
) AS t;
```

La subconsulta genera una tabla temporal con dos columnas:

| IdCliente | TotalGastado |
| ----------: | -------------: |

La consulta exterior simplemente muestra ese resultado.

---

## Filtrando la tabla temporal

Una vez creada la tabla temporal podemos aplicar filtros.

```sql
SELECT *
FROM
(
    SELECT
        IdCliente,
        SUM(Total) AS TotalGastado
    FROM Pedido
    GROUP BY IdCliente
) AS t
WHERE TotalGastado > 5000;
```

Aquí primero se calcula el gasto de todos los clientes y posteriormente solo se muestran aquellos cuyo gasto supera los 5000 euros.

---

## Ordenando el resultado

También podemos ordenar la tabla temporal.

```sql
SELECT *
FROM
(
    SELECT
        IdCliente,
        SUM(Total) AS TotalGastado
    FROM Pedido
    GROUP BY IdCliente
) AS t
ORDER BY TotalGastado DESC;
```

Esto permite construir informes muy fácilmente.

---

## ¿Por qué no utilizar directamente GROUP BY?

En algunos casos basta con una única consulta.

Sin embargo, cuando necesitamos seguir trabajando sobre el resultado de una agregación, una subconsulta en `FROM` hace que la consulta sea mucho más clara.

Por ejemplo:

1. calcular ventas por cliente;
2. ordenar;
3. filtrar;
4. unir posteriormente con otras tablas.

---

## Derivadas o tablas derivadas

Las subconsultas en `FROM` reciben habitualmente el nombre de:

* **tabla derivada** (​*Derived Table*​).

Porque generan una tabla nueva derivada del resultado de otra consulta.

Aunque esa tabla no existe físicamente en la base de datos, MySQL la trata como si existiera durante la ejecución de la consulta.

---

## Aplicaciones reales

Las tablas derivadas aparecen con frecuencia en:

* informes comerciales;
* cuadros de mando;
* estadísticas;
* análisis de ventas;
* rankings;
* informes financieros.

En muchos casos constituyen la forma más sencilla de dividir un problema complejo en varias etapas.

---

## Buenas prácticas

* Asigna siempre un alias descriptivo a la tabla derivada.
* Evita utilizar `SELECT *` dentro de la subconsulta si no es necesario.
* Devuelve únicamente las columnas que realmente utilizará la consulta exterior.
* Utiliza nombres claros para las columnas calculadas (`TotalVentas`, `MediaPrecio`, etc.).

---

## Ideas clave

* Una subconsulta en `FROM` genera una tabla temporal.
* Esa tabla puede consultarse igual que cualquier otra.
* Es obligatorio asignarle un alias.
* Resulta muy útil para construir consultas complejas en varias etapas.

