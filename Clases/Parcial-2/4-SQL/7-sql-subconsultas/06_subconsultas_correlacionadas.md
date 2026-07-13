# Subconsultas correlacionadas

## Introducción

Hasta este momento todas las subconsultas que hemos estudiado tenían una característica común:

​**podían ejecutarse de forma independiente**​.

Por ejemplo:

```sql
SELECT AVG(Precio)
FROM Producto;
```

Puede ejecutarse sola y devuelve un resultado perfectamente válido.

Sin embargo, existe un tipo de subconsulta mucho más potente cuyo resultado ​**depende de cada fila que está procesando la consulta principal**​.

A estas consultas las denominamos ​**subconsultas correlacionadas**​.

Son uno de los conceptos más importantes del SQL avanzado.

---

## ¿Qué significa "correlacionada"?

Significa que la subconsulta utiliza datos de la consulta exterior.

Es decir, ambas consultas están conectadas.

Visualmente:

```text
Consulta Principal

Fila 1
   │
   ▼
Subconsulta

Fila 2
   │
   ▼
Subconsulta

Fila 3
   │
   ▼
Subconsulta

...
```

La subconsulta no se ejecuta una sola vez.

Se ejecuta una vez por cada fila procesada por la consulta principal.

---

## Primer ejemplo

Supongamos las siguientes tablas:

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
|      102 |         1 |
|      103 |         3 |

Queremos mostrar el número de pedidos de cada cliente.

Podemos escribir:

```sql
SELECT
    c.Nombre,
    (
        SELECT COUNT(*)
        FROM Pedido p
        WHERE p.IdCliente = c.IdCliente
    ) AS TotalPedidos
FROM Cliente c;
```

Observa la condición:

```sql
p.IdCliente = c.IdCliente
```

La subconsulta utiliza una columna de la consulta principal.

Por eso está correlacionada.

---

## ¿Cómo ejecuta MySQL esta consulta?

Conceptualmente, el proceso es:

Para Ana:

```sql
SELECT COUNT(*)
FROM Pedido
WHERE IdCliente = 1;
```

Resultado:

```text
2
```

Para Luis:

```sql
SELECT COUNT(*)
FROM Pedido
WHERE IdCliente = 2;
```

Resultado:

```text
0
```

Para Marta:

```sql
SELECT COUNT(*)
FROM Pedido
WHERE IdCliente = 3;
```

Resultado:

```text
1
```

Finalmente:

| Cliente | Pedidos |
| --------- | --------: |
| Ana     |       2 |
| Luis    |       0 |
| Marta   |       1 |

---

## Otro ejemplo

Mostrar el importe total comprado por cada cliente.

```sql
SELECT
    c.Nombre,
    (
        SELECT SUM(Total)
        FROM Pedido p
        WHERE p.IdCliente = c.IdCliente
    ) AS TotalComprado
FROM Cliente c;
```

Cada cliente obtiene un resultado diferente.

---

## Diferencia respecto a una subconsulta simple

Subconsulta simple:

```sql
SELECT AVG(Precio)
FROM Producto;
```

Se ejecuta:

**una sola vez.**

Subconsulta correlacionada:

```sql
SELECT ...
FROM Cliente
```

↓

```sql
SELECT COUNT(*)
FROM Pedido
WHERE Pedido.IdCliente = Cliente.IdCliente;
```

Se ejecuta:

**una vez por cada cliente.**

Esta diferencia es fundamental.

---

## Ventajas

Las subconsultas correlacionadas permiten calcular fácilmente:

* número de pedidos de cada cliente;
* total vendido por empleado;
* cantidad de productos por categoría;
* última compra de cada cliente;
* salario medio de cada departamento.

Son muy utilizadas en informes empresariales.

---

## Inconvenientes

Como la subconsulta puede ejecutarse miles de veces, este tipo de consultas puede resultar más lento que una solución basada en `JOIN` y `GROUP BY`.

Más adelante veremos cuándo conviene utilizar una u otra técnica.

---

## Buenas prácticas

Utiliza subconsultas correlacionadas cuando:

* cada fila necesita un cálculo distinto;
* el código resulte más claro que utilizando varios `JOIN`;
* el rendimiento siga siendo aceptable.

Si la consulta procesa millones de registros, suele ser recomendable estudiar alternativas.

---

## Ideas clave

* Una subconsulta correlacionada depende de la consulta principal.
* Se ejecuta una vez por cada fila procesada.
* Permite realizar cálculos personalizados para cada registro.
* Es una herramienta muy potente, aunque puede tener un mayor coste de ejecución.

