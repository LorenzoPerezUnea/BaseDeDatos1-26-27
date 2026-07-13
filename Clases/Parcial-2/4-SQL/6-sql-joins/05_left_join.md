# LEFT JOIN

## Introducción

Aunque `INNER JOIN` es el tipo de unión más utilizado, presenta una limitación importante:

**descarta los registros que no encuentran correspondencia en la otra tabla.**

En muchas ocasiones precisamente queremos localizar esos registros "sin pareja".

Por ejemplo:

* clientes que todavía no han realizado ningún pedido;
* empleados sin departamento asignado;
* productos que nunca se han vendido.

Para resolver este problema utilizaremos ​**`LEFT JOIN`**​.

---

## ¿Qué hace LEFT JOIN?

`LEFT JOIN` devuelve:

* ​**todas las filas de la tabla situada a la izquierda**​;
* únicamente las filas coincidentes de la tabla situada a la derecha.

Cuando no existe coincidencia, SQL rellena las columnas de la segunda tabla con valores `NULL`.

---

## Representación mediante conjuntos

```text
Tabla A

     ███████████
   ███████████████
  █████████████████
  ███████████
   ███████████████
     ███████████

        Tabla B
```

La zona sombreada representa:

* toda la tabla izquierda;
* más la intersección.

---

## Ejemplo

Supongamos:

### Cliente

| Id | Nombre |
| ---: | -------- |
|  1 | Ana    |
|  2 | Luis   |
|  3 | Marta  |

### Pedido

| Pedido | IdCliente |
| -------: | ----------: |
|    101 |         1 |
|    102 |         3 |

Consulta:

```sql
SELECT
    c.Nombre,
    p.IdPedido
FROM Cliente AS c
LEFT JOIN Pedido AS p
ON c.IdCliente = p.IdCliente;
```

Resultado:

| Nombre | Pedido |
| -------- | -------: |
| Ana    |    101 |
| Luis   |   NULL |
| Marta  |    102 |

Ahora Luis sí aparece en el resultado.

La ausencia de pedidos se representa mediante `NULL`.

---

## ¿Para qué sirve?

Uno de los usos más habituales consiste en localizar registros que no tienen relación con otra tabla.

Por ejemplo:

```sql
SELECT
    c.Nombre
FROM Cliente AS c
LEFT JOIN Pedido AS p
ON c.IdCliente = p.IdCliente
WHERE p.IdPedido IS NULL;
```

Resultado:

| Nombre |
| -------- |
| Luis   |

Esta consulta obtiene todos los clientes que todavía no han realizado ningún pedido.

Es uno de los patrones más utilizados en SQL profesional.

---

## Orden de las tablas

En un `LEFT JOIN` el orden sí importa.

```sql
Cliente
LEFT JOIN Pedido
```

no produce el mismo resultado que

```sql
Pedido
LEFT JOIN Cliente
```

La tabla situada a la izquierda es la que se conserva completamente.

Por este motivo es importante elegir correctamente cuál será la tabla principal de la consulta.

---

## Aplicaciones reales

`LEFT JOIN` resulta especialmente útil para:

* detectar clientes sin pedidos;
* localizar productos sin ventas;
* encontrar empleados sin proyectos asignados;
* identificar categorías vacías;
* buscar registros huérfanos.

Estas consultas son habituales en tareas de auditoría y mantenimiento de bases de datos.

---

## Ideas clave

* `LEFT JOIN` conserva todas las filas de la tabla izquierda.
* Cuando no existe coincidencia, las columnas de la tabla derecha contienen `NULL`.
* Es especialmente útil para localizar registros sin relación.
* El orden de las tablas influye directamente en el resultado.
* Es uno de los tipos de unión más utilizados después de `INNER JOIN`.

