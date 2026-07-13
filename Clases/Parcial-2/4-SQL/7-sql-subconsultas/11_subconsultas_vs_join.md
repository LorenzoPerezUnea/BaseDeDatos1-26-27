# Subconsultas vs JOIN

## Introducción

Llegados a este punto surge una pregunta muy habitual:

> **¿Cuándo debo utilizar una subconsulta y cuándo un JOIN?**

La respuesta es importante porque, en muchos casos, ambos enfoques permiten resolver el mismo problema.

Sin embargo, cada uno tiene ventajas e inconvenientes.

Aprender a elegir la mejor opción es una habilidad propia de un desarrollador con experiencia.

---

## Un mismo problema

Queremos mostrar todos los clientes que han realizado al menos un pedido.

### Solución mediante JOIN

```sql
SELECT DISTINCT
    c.Nombre
FROM Cliente AS c
INNER JOIN Pedido AS p
ON c.IdCliente = p.IdCliente;
```

La consulta une ambas tablas y elimina duplicados mediante `DISTINCT`.

---

### Solución mediante EXISTS

```sql
SELECT
    c.Nombre
FROM Cliente AS c
WHERE EXISTS
(
    SELECT 1
    FROM Pedido AS p
    WHERE p.IdCliente = c.IdCliente
);
```

El resultado es exactamente el mismo.

---

## Otro ejemplo

Queremos mostrar los productos cuyo precio es superior a la media.

Mediante subconsulta:

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

Intentar resolver este problema únicamente con un `JOIN` sería mucho más complicado y menos intuitivo.

Aquí la subconsulta es claramente la mejor opción.

---

## ¿Cuándo utilizar JOIN?

Los `JOIN` son la mejor elección cuando:

* necesitamos combinar información de varias tablas;
* queremos mostrar columnas procedentes de distintas tablas;
* trabajamos con relaciones entre entidades;
* necesitamos recuperar información distribuida en el modelo relacional.

Ejemplos:

* cliente + pedido;
* pedido + producto;
* empleado + departamento.

---

## ¿Cuándo utilizar subconsultas?

Las subconsultas resultan especialmente adecuadas cuando:

* necesitamos calcular un valor antes de realizar una comparación;
* queremos filtrar utilizando resultados agregados;
* debemos comprobar la existencia de registros (`EXISTS`);
* necesitamos construir tablas derivadas (`FROM`);
* cada fila requiere un cálculo independiente (subconsultas correlacionadas).

---

## Rendimiento

En versiones modernas de MySQL, el optimizador suele transformar internamente muchas subconsultas en planes de ejecución muy similares a los obtenidos mediante `JOIN`.

Por ello, no siempre existe una diferencia significativa de rendimiento.

No obstante:

* un `JOIN` mal construido puede generar millones de filas innecesarias;
* una subconsulta correlacionada sobre millones de registros puede ejecutarse miles de veces.

Por eso es importante analizar siempre el problema concreto.

---

## Legibilidad

En muchas ocasiones el criterio más importante no es el rendimiento, sino la claridad del código.

Compara estas dos ideas:

> "Mostrar clientes que tienen pedidos."

Con `EXISTS`, la consulta expresa exactamente esa intención.

En cambio, un `JOIN` puede requerir `DISTINCT` para eliminar duplicados, haciendo la consulta algo menos directa.

Elegir la solución más fácil de entender también es una buena práctica.

---

## Recomendaciones

Como norma general:

* utiliza `JOIN` para combinar datos de distintas tablas;
* utiliza subconsultas para realizar cálculos o comprobaciones;
* utiliza `EXISTS` cuando únicamente quieras saber si una relación existe;
* no intentes resolver todos los problemas utilizando siempre la misma técnica.

Un buen desarrollador conoce varias soluciones y selecciona la más adecuada en cada situación.

---

## Resumen comparativo

| JOIN                              | Subconsultas                                         |
| ----------------------------------- | ------------------------------------------------------ |
| Combinan tablas                   | Calculan resultados                                  |
| Recuperan columnas relacionadas   | Filtran o generan nuevos valores                     |
| Muy utilizados en informes        | Muy utilizadas en análisis y validaciones           |
| Pueden generar duplicados         | Suelen expresar mejor ciertas condiciones            |
| Ideales para mostrar información | Ideales para realizar comparaciones y comprobaciones |

---

## Ideas clave

* `JOIN` y subconsultas no son rivales; son herramientas complementarias.
* La elección depende del problema que se desea resolver.
* Los `JOIN` destacan al combinar información de varias tablas.
* Las subconsultas destacan al calcular valores y realizar comprobaciones.
* Conocer ambas técnicas permite escribir consultas más claras, eficientes y fáciles de mantener.

