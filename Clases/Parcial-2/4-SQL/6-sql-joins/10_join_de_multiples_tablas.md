# JOIN de múltiples tablas

## Introducción

Hasta ahora todas las consultas han relacionado únicamente ​**dos tablas**​.

Sin embargo, en una base de datos real es muy poco frecuente trabajar solamente con dos tablas.

Lo habitual es que una consulta combine información procedente de tres, cuatro, cinco o incluso más tablas relacionadas.

Afortunadamente, SQL permite encadenar tantos `JOIN` como sean necesarios.

Comprender este mecanismo es uno de los pasos que separan las consultas básicas de las consultas profesionales.

---

## Un ejemplo de una empresa

Supongamos el siguiente modelo simplificado.

```text
Cliente

IdCliente
Nombre

      │

      ▼

Pedido

IdPedido
Fecha
IdCliente

      │

      ▼

DetallePedido

IdPedido
IdProducto
Cantidad

      │

      ▼

Producto

IdProducto
Nombre
IdCategoria

      │

      ▼

Categoria

IdCategoria
Nombre
```

Cada tabla aporta una parte de la información.

---

## La consulta

Queremos obtener un informe con:

* nombre del cliente;
* fecha del pedido;
* producto comprado;
* categoría del producto;
* cantidad adquirida.

La consulta sería:

```sql
SELECT
    c.Nombre AS Cliente,
    p.Fecha,
    pr.Nombre AS Producto,
    ca.Nombre AS Categoria,
    dp.Cantidad
FROM Cliente AS c

INNER JOIN Pedido AS p
    ON c.IdCliente = p.IdCliente

INNER JOIN DetallePedido AS dp
    ON p.IdPedido = dp.IdPedido

INNER JOIN Producto AS pr
    ON dp.IdProducto = pr.IdProducto

INNER JOIN Categoria AS ca
    ON pr.IdCategoria = ca.IdCategoria;
```

Aunque la consulta parece larga, sigue exactamente el mismo patrón:

1. añadir una tabla;
2. indicar cómo se relaciona con la anterior mediante `ON`;
3. repetir el proceso.

---

## Analizando el recorrido

Podemos interpretar la consulta como un recorrido por el modelo relacional.

```text
Cliente

↓

Pedido

↓

DetallePedido

↓

Producto

↓

Categoría
```

Cada `JOIN` permite avanzar un paso más.

Este modo de pensar facilita enormemente el diseño de consultas complejas.

---

## Utilizando LEFT JOIN

No siempre todos los registros tienen información asociada.

Por ejemplo, podríamos querer mostrar todas las categorías, incluso aquellas que todavía no tienen productos.

En ese caso bastaría con sustituir uno de los `INNER JOIN` por un `LEFT JOIN`.

```sql
SELECT
    ca.Nombre,
    pr.Nombre
FROM Categoria AS ca

LEFT JOIN Producto AS pr
ON ca.IdCategoria = pr.IdCategoria;
```

La elección del tipo de `JOIN` depende del resultado que deseemos obtener.

---

## Mezclando distintos JOIN

Una misma consulta puede combinar varios tipos.

Por ejemplo:

```sql
FROM Cliente AS c

INNER JOIN Pedido AS p
ON c.IdCliente = p.IdCliente

LEFT JOIN Factura AS f
ON p.IdPedido = f.IdPedido

INNER JOIN Empleado AS e
ON p.IdEmpleado = e.IdEmpleado
```

No existe ninguna limitación.

Cada unión puede utilizar el tipo más adecuado para esa parte de la consulta.

---

## Consultas largas

En aplicaciones empresariales es habitual encontrar consultas con:

* 8 tablas;
* 12 tablas;
* incluso más de 20 tablas.

Por este motivo resulta fundamental mantener una buena organización.

---

## Buenas prácticas

Cuando una consulta contiene muchos `JOIN` es recomendable:

* utilizar alias cortos y descriptivos;
* escribir un `JOIN` por línea;
* alinear las cláusulas `ON`;
* mantener el mismo orden que sigue el modelo relacional;
* evitar seleccionar columnas innecesarias utilizando `SELECT *`.

Estas prácticas facilitan enormemente la lectura y el mantenimiento.

---

## Ideas clave

* SQL permite encadenar tantos `JOIN` como sea necesario.
* Cada `JOIN` incorpora una nueva tabla al resultado.
* Una consulta compleja suele seguir el recorrido de las relaciones del modelo relacional.
* Es posible combinar distintos tipos de `JOIN` en una misma consulta.
* Una buena organización mejora considerablemente la legibilidad de consultas extensas.

