# EXISTS

## Introducción

En muchas ocasiones no necesitamos conocer un valor concreto.

Lo único que queremos saber es si ​**existe al menos un registro que cumpla una determinada condición**​.

Para este tipo de problemas SQL proporciona el operador ​**`EXISTS`**​.

En lugar de devolver datos, `EXISTS` responde a una pregunta muy sencilla:

> **¿Existe alguna fila que cumpla esta condición?**

La respuesta siempre será:

* verdadero (`TRUE`);
* falso (`FALSE`).

---

## Sintaxis

```sql
SELECT
    columnas
FROM TablaPrincipal t
WHERE EXISTS
(
    SELECT *
    FROM OtraTabla o
    WHERE ...
);
```

La subconsulta suele estar correlacionada con la consulta principal.

---

## Primer ejemplo

Queremos mostrar únicamente los clientes que han realizado al menos un pedido.

```sql
SELECT
    c.Nombre
FROM Cliente c
WHERE EXISTS
(
    SELECT *
    FROM Pedido p
    WHERE p.IdCliente = c.IdCliente
);
```

Para cada cliente MySQL comprueba:

> ¿Existe algún pedido cuyo `IdCliente` coincida?

Si la respuesta es sí, el cliente aparece en el resultado.

---

## Funcionamiento paso a paso

Para Ana:

```sql
SELECT *
FROM Pedido
WHERE IdCliente = 1;
```

Devuelve registros.

Resultado:

```text
TRUE
```

Ana aparece.

---

Para Luis:

```sql
SELECT *
FROM Pedido
WHERE IdCliente = 2;
```

No devuelve registros.

Resultado:

```text
FALSE
```

Luis no aparece.

---

## ¿Por qué suele utilizarse SELECT \*?

Es frecuente encontrar:

```sql
SELECT *
```

o incluso:

```sql
SELECT 1
```

Dentro de `EXISTS`.

En realidad, el contenido del `SELECT`​**es irrelevante**​.

`EXISTS` no utiliza esos datos.

Únicamente comprueba si la subconsulta devuelve alguna fila.

Por ello son equivalentes:

```sql
SELECT *
```

```sql
SELECT 1
```

```sql
SELECT IdPedido
```

---

## Ventajas

`EXISTS` presenta varias ventajas:

* expresa claramente la intención de la consulta;
* suele ser muy eficiente;
* MySQL puede dejar de buscar en cuanto encuentra la primera coincidencia.

No necesita recorrer todas las filas.

---

## Casos de uso

`EXISTS` se utiliza habitualmente para responder preguntas como:

* ¿Qué clientes han realizado compras?
* ¿Qué empleados tienen proyectos asignados?
* ¿Qué productos aparecen en algún pedido?
* ¿Qué categorías contienen productos?

En todos estos casos únicamente interesa saber si existe alguna relación.

---

## EXISTS frente a COUNT()

Muchos principiantes escriben:

```sql
SELECT COUNT(*)
```

para comprobar si existen registros.

Sin embargo, `COUNT()` necesita contar todas las filas.

`EXISTS` puede detener la búsqueda en la primera coincidencia, por lo que normalmente resulta más eficiente.

---

## Ideas clave

* `EXISTS` devuelve `TRUE` cuando la subconsulta devuelve al menos una fila.
* Generalmente se utiliza con subconsultas correlacionadas.
* El contenido del `SELECT` es irrelevante; lo importante es la existencia de filas.
* En muchos casos ofrece un mejor rendimiento que utilizar `COUNT()` para comprobar la existencia de registros.

