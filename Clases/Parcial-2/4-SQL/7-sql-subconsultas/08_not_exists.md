# NOT EXISTS

## Introducción

Si `EXISTS` responde a la pregunta:

> **¿Existe algún registro relacionado?**

`NOT EXISTS` responde justamente a la pregunta contraria:

> **¿No existe ningún registro relacionado?**

Es uno de los operadores más utilizados en bases de datos empresariales para localizar información que falta o detectar situaciones anómalas.

Mientras que `EXISTS` busca relaciones existentes, `NOT EXISTS` encuentra ​**ausencias de relaciones**​.

---

## Sintaxis

```sql
SELECT
    columnas
FROM TablaPrincipal t
WHERE NOT EXISTS
(
    SELECT 1
    FROM OtraTabla o
    WHERE ...
);
```

Como ocurría con `EXISTS`, la subconsulta suele estar correlacionada con la consulta principal.

---

## Primer ejemplo

Queremos encontrar los clientes que todavía no han realizado ningún pedido.

```sql
SELECT
    c.IdCliente,
    c.Nombre
FROM Cliente AS c
WHERE NOT EXISTS
(
    SELECT 1
    FROM Pedido AS p
    WHERE p.IdCliente = c.IdCliente
);
```

Proceso:

Para cada cliente:

* MySQL busca pedidos asociados.
* Si encuentra alguno → `EXISTS = TRUE`.
* `NOT EXISTS` lo convierte en `FALSE`.
* Ese cliente no aparece.

Si no encuentra ninguno:

* `EXISTS = FALSE`.
* `NOT EXISTS = TRUE`.
* El cliente aparece en el resultado.

---

## Resultado

Supongamos:

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

Consulta:

```sql
SELECT
    c.Nombre
FROM Cliente c
WHERE NOT EXISTS
(
    SELECT 1
    FROM Pedido p
    WHERE p.IdCliente = c.IdCliente
);
```

Resultado:

| Nombre |
| -------- |
| Luis   |

Luis nunca ha realizado un pedido.

---

## Otros ejemplos reales

### Productos nunca vendidos

```sql
SELECT
    pr.Nombre
FROM Producto pr
WHERE NOT EXISTS
(
    SELECT 1
    FROM DetallePedido dp
    WHERE dp.IdProducto = pr.IdProducto
);
```

---

### Empleados sin pedidos asignados

```sql
SELECT
    e.Nombre
FROM Empleado e
WHERE NOT EXISTS
(
    SELECT 1
    FROM Pedido p
    WHERE p.IdEmpleado = e.IdEmpleado
);
```

---

### Categorías vacías

```sql
SELECT
    c.Nombre
FROM Categoria c
WHERE NOT EXISTS
(
    SELECT 1
    FROM Producto p
    WHERE p.IdCategoria = c.IdCategoria
);
```

Este tipo de consultas es muy habitual en tareas de mantenimiento y auditoría.

---

## NOT EXISTS frente a LEFT JOIN

Muchos problemas pueden resolverse de ambas maneras.

Por ejemplo:

Clientes sin pedidos.

Con `LEFT JOIN`:

```sql
SELECT
    c.Nombre
FROM Cliente c
LEFT JOIN Pedido p
ON c.IdCliente = p.IdCliente
WHERE p.IdPedido IS NULL;
```

Con `NOT EXISTS`:

```sql
SELECT
    c.Nombre
FROM Cliente c
WHERE NOT EXISTS
(
    SELECT 1
    FROM Pedido p
    WHERE p.IdCliente = c.IdCliente
);
```

Ambas consultas producen el mismo resultado.

En muchos motores de bases de datos el optimizador transforma ambas internamente en planes de ejecución muy similares.

---

## ¿Cuándo utilizar NOT EXISTS?

Es especialmente recomendable cuando la pregunta puede formularse de esta manera:

* ¿Qué clientes **no tienen** pedidos?
* ¿Qué productos **no aparecen** en ventas?
* ¿Qué empleados **no pertenecen** a ningún proyecto?
* ¿Qué alumnos **no han entregado** una práctica?

Si el problema consiste en localizar la ausencia de registros relacionados, `NOT EXISTS` suele ser la opción más expresiva.

---

## Ideas clave

* `NOT EXISTS` devuelve `TRUE` cuando la subconsulta no devuelve ninguna fila.
* Es ideal para localizar registros sin relaciones.
* Se utiliza frecuentemente en auditorías y controles de calidad de datos.
* En muchos casos puede sustituir a un `LEFT JOIN ... IS NULL`.
* Expresa de forma muy clara la intención de la consulta.

