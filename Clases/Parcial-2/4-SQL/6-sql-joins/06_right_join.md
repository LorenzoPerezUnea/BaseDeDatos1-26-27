# RIGHT JOIN

## Introducción

Después de estudiar `LEFT JOIN`, el funcionamiento de `RIGHT JOIN` resulta muy sencillo de comprender.

En realidad, ambos realizan exactamente la misma operación, pero conservando tablas distintas.

Mientras que `LEFT JOIN` mantiene todas las filas de la tabla situada a la izquierda, `RIGHT JOIN` conserva todas las filas de la tabla situada a la derecha.

Aunque MySQL implementa `RIGHT JOIN`, muchos desarrolladores prefieren escribir siempre consultas utilizando `LEFT JOIN`, simplemente intercambiando el orden de las tablas. Esto hace que el código sea más uniforme y fácil de leer.

---

## ¿Qué hace RIGHT JOIN?

`RIGHT JOIN` devuelve:

* todas las filas de la tabla situada a la derecha;
* únicamente las filas relacionadas de la tabla situada a la izquierda.

Cuando una fila de la tabla derecha no encuentra correspondencia, las columnas de la tabla izquierda aparecen con el valor `NULL`.

---

## Representación mediante conjuntos

```text
Tabla A

     ○──────────○
   ○              ███
  ○      ████████████
  ○      ████████████
   ○              ███
     ○──────────○
        Tabla B
```

La zona sombreada representa:

* toda la tabla derecha;
* la intersección.

---

## Ejemplo

Supongamos las siguientes tablas.

### Cliente

| IdCliente | Nombre |
| ----------: | -------- |
|         1 | Ana    |
|         2 | Luis   |

### Pedido

| IdPedido | IdCliente |
| ---------: | ----------: |
|      101 |         1 |
|      102 |         3 |

Observemos que el pedido 102 hace referencia a un cliente que ya no existe (suponiendo que la integridad referencial no estuviera activa).

Consulta:

```sql
SELECT
    c.Nombre,
    p.IdPedido
FROM Cliente AS c
RIGHT JOIN Pedido AS p
ON c.IdCliente = p.IdCliente;
```

Resultado:

| Nombre | IdPedido |
| -------- | ---------: |
| Ana    |      101 |
| NULL   |      102 |

Todos los pedidos aparecen, incluso aquellos cuyo cliente no existe.

---

## Equivalencia con LEFT JOIN

La consulta anterior puede escribirse utilizando `LEFT JOIN`.

```sql
SELECT
    c.Nombre,
    p.IdPedido
FROM Pedido AS p
LEFT JOIN Cliente AS c
ON p.IdCliente = c.IdCliente;
```

El resultado es exactamente el mismo.

Por este motivo muchos equipos de desarrollo deciden utilizar exclusivamente `LEFT JOIN` en todos sus proyectos.

---

## ¿Cuándo utilizar RIGHT JOIN?

Puede resultar útil cuando la tabla principal de la consulta es la situada a la derecha y queremos mantener esa estructura por motivos de legibilidad.

Sin embargo, en la práctica profesional suele ser más habitual reorganizar la consulta y utilizar `LEFT JOIN`.

---

## Ventajas y desventajas

### Ventajas

* Permite conservar la tabla derecha.
* Su sintaxis es sencilla.
* Forma parte del estándar SQL.

### Desventajas

* Muchas consultas resultan menos intuitivas.
* Puede dificultar la lectura cuando intervienen numerosas tablas.
* Es fácilmente reemplazable mediante `LEFT JOIN`.

---

## Buenas prácticas

En proyectos pequeños cualquiera de los dos estilos es válido.

En proyectos grandes es recomendable mantener un único criterio.

Muchos equipos establecen la siguiente norma:

* utilizar siempre `LEFT JOIN`;
* ordenar las tablas de manera que la principal aparezca a la izquierda.

Esto reduce la complejidad al leer consultas extensas.

---

## Ideas clave

* `RIGHT JOIN` conserva todas las filas de la tabla derecha.
* Las filas sin correspondencia generan valores `NULL` en la tabla izquierda.
* Puede reescribirse fácilmente utilizando `LEFT JOIN`.
* Su uso es correcto, aunque en muchos proyectos se prefiere trabajar únicamente con `LEFT JOIN`.

