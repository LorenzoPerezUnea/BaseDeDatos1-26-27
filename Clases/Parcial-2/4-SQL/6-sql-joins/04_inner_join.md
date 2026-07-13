# INNER JOIN

## Introducción

Después de comprender el concepto de producto cartesiano ya estamos preparados para estudiar el tipo de unión más importante de SQL:

​**`INNER JOIN`**​.

Cuando un desarrollador habla simplemente de "hacer un JOIN", en la mayoría de los casos se está refiriendo precisamente a un `INNER JOIN`.

Es el tipo de unión más utilizado en aplicaciones empresariales porque devuelve únicamente la información que está relacionada en ambas tablas.

---

## ¿Qué hace INNER JOIN?

`INNER JOIN` compara las filas de dos tablas utilizando una condición de unión.

Solo aquellas filas que cumplen dicha condición aparecen en el resultado.

Visualmente:

```text
Cliente                Pedido

Ana                    Pedido 101
Luis                   Pedido 102
Marta                  Pedido 103

        │
        │ INNER JOIN
        ▼

Solo las filas relacionadas
```

Las filas que no encuentran correspondencia son descartadas.

---

## Representación mediante conjuntos

Una forma muy habitual de representar un `INNER JOIN` es utilizando diagramas de Venn.

```text
Tabla A

     ○──────────○
   ○              ○
  ○      ███       ○
  ○      ███       ○
   ○              ○
     ○──────────○
        Tabla B
```

La zona sombreada representa únicamente la intersección.

Solo se conservan los registros presentes en ambas tablas.

---

## Sintaxis

La sintaxis general es:

```sql
SELECT
    columnas
FROM TablaA
INNER JOIN TablaB
ON TablaA.Clave = TablaB.Clave;
```

La cláusula `ON` especifica la condición utilizada para relacionar ambas tablas.

---

## Primer ejemplo

Supongamos las siguientes tablas.

### Cliente

| IdCliente | Nombre |
| ----------: | -------- |
|         1 | Ana    |
|         2 | Luis   |
|         3 | Marta  |

### Pedido

| IdPedido | IdCliente |
| ---------: | ----------: |
|      101 |         1 |
|      102 |         3 |
|      103 |         1 |

Consulta:

```sql
SELECT
    Cliente.Nombre,
    Pedido.IdPedido
FROM Cliente
INNER JOIN Pedido
ON Cliente.IdCliente = Pedido.IdCliente;
```

Resultado:

| Nombre | Pedido |
| -------- | -------: |
| Ana    |    101 |
| Ana    |    103 |
| Marta  |    102 |

Observemos que ​**Luis no aparece**​, ya que no tiene ningún pedido asociado.

---

## Analizando paso a paso

Internamente el proceso puede entenderse de la siguiente forma:

1. Se consideran ambas tablas.
2. Se comparan todos los valores de `Cliente.IdCliente` con `Pedido.IdCliente`.
3. Solo se conservan las coincidencias.
4. Se construye una tabla temporal con las columnas solicitadas.

Aunque el motor de MySQL utiliza algoritmos mucho más eficientes que un producto cartesiano completo, conceptualmente este modelo resulta muy útil para comprender el funcionamiento del `JOIN`.

---

## INNER JOIN con varias columnas

Podemos seleccionar cualquier combinación de columnas.

```sql
SELECT
    Cliente.Nombre,
    Pedido.IdPedido,
    Pedido.Fecha
FROM Cliente
INNER JOIN Pedido
ON Cliente.IdCliente = Pedido.IdCliente;
```

El resultado combina información procedente de ambas tablas como si perteneciera a una única relación.

---

## Utilizando alias

Cuando las consultas empiezan a crecer es recomendable utilizar alias.

```sql
SELECT
    c.Nombre,
    p.IdPedido,
    p.Fecha
FROM Cliente AS c
INNER JOIN Pedido AS p
ON c.IdCliente = p.IdCliente;
```

Los alias reducen considerablemente la longitud de las consultas y mejoran su legibilidad.

---

## INNER JOIN con filtros

El `JOIN` puede combinarse con cualquier cláusula que ya conocemos.

```sql
SELECT
    c.Nombre,
    p.IdPedido,
    p.Fecha
FROM Cliente AS c
INNER JOIN Pedido AS p
ON c.IdCliente = p.IdCliente
WHERE p.Fecha >= '2026-01-01'
ORDER BY p.Fecha;
```

En este ejemplo:

* primero se realiza la unión;
* después se filtran los pedidos;
* finalmente se ordenan los resultados.

---

## INNER JOIN con funciones de agregación

También podemos combinar `INNER JOIN` con `GROUP BY`.

Por ejemplo, contar cuántos pedidos ha realizado cada cliente.

```sql
SELECT
    c.Nombre,
    COUNT(*) AS TotalPedidos
FROM Cliente AS c
INNER JOIN Pedido AS p
ON c.IdCliente = p.IdCliente
GROUP BY c.Nombre;
```

Resultado:

| Cliente | TotalPedidos |
| --------- | -------------: |
| Ana     |            2 |
| Marta   |            1 |

Luis no aparece porque no tiene pedidos.

---

## Aplicaciones reales

`INNER JOIN` aparece constantemente en aplicaciones reales.

Por ejemplo:

* pedidos junto al nombre del cliente;
* productos con su categoría;
* empleados con su departamento;
* facturas con el vendedor responsable;
* matrículas con la información del estudiante;
* reservas con los datos del huésped.

Prácticamente cualquier consulta profesional utiliza uno o varios `INNER JOIN`.

---

## Buenas prácticas

Cuando utilices `INNER JOIN` recuerda:

* utilizar siempre alias cuando intervengan varias tablas;
* escribir explícitamente `INNER JOIN` aunque pueda omitirse la palabra `INNER`;
* seleccionar únicamente las columnas necesarias;
* comprobar que la condición del `ON` relaciona correctamente las tablas.

---

## Ideas clave

* `INNER JOIN` devuelve únicamente las filas relacionadas en ambas tablas.
* Es el tipo de unión más utilizado en SQL.
* La condición de unión se especifica mediante `ON`.
* Puede combinarse con `WHERE`, `GROUP BY`, `HAVING` y `ORDER BY`.
* Constituye la base de la mayoría de consultas empresariales.

