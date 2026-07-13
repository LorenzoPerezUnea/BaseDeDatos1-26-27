# ¿Por qué necesitamos los JOIN?

## Introducción

Una de las características fundamentales del modelo relacional es que la información ​**no se almacena toda junta**​, sino distribuida en múltiples tablas.

Esta separación evita duplicidades y facilita el mantenimiento de la base de datos.

Sin embargo, también implica que para responder muchas preguntas debemos ​**reunir información procedente de varias tablas**​.

Ese es precisamente el objetivo de los `JOIN`.

---

## Un ejemplo cotidiano

Supongamos una empresa con dos tablas.

### Cliente

| IdCliente | Nombre |
| ----------: | -------- |
|         1 | Ana    |
|         2 | Luis   |
|         3 | Marta  |

### Pedido

| IdPedido | IdCliente | Fecha      |
| ---------: | ----------: | ------------ |
|      101 |         1 | 2026-01-10 |
|      102 |         3 | 2026-01-15 |
|      103 |         1 | 2026-02-02 |

Observa que la tabla `Pedido`​**no almacena el nombre del cliente**​.

Únicamente almacena su identificador.

Esto evita repetir miles de veces el nombre del cliente en cada pedido.

---

## El problema

Si queremos responder:

> ¿Qué cliente realizó cada pedido?

Ninguna tabla contiene toda la información.

La tabla Cliente conoce el nombre.

La tabla Pedido conoce la fecha.

Necesitamos combinar ambas.

---

## Una primera idea (incorrecta)

Algunos principiantes intentan resolverlo realizando dos consultas independientes.

```sql
SELECT *
FROM Cliente;
```

y

```sql
SELECT *
FROM Pedido;
```

Pero ahora el trabajo de relacionar ambas tablas recaería sobre el programador o incluso sobre el usuario.

SQL puede hacerlo automáticamente.

---

## La solución

Relacionamos ambas tablas mediante la clave foránea.

```sql
SELECT
    Cliente.Nombre,
    Pedido.IdPedido,
    Pedido.Fecha
FROM Cliente
INNER JOIN Pedido
ON Cliente.IdCliente = Pedido.IdCliente;
```

Resultado:

| Cliente | Pedido | Fecha      |
| --------- | -------: | ------------ |
| Ana     |    101 | 2026-01-10 |
| Marta   |    102 | 2026-01-15 |
| Ana     |    103 | 2026-02-02 |

Ahora la información aparece como si procediera de una única tabla.

En realidad, SQL ha combinado dinámicamente ambas relaciones.

---

## ¿Qué hace realmente un JOIN?

Conceptualmente un JOIN:

* toma dos tablas;
* compara determinadas columnas;
* encuentra las filas relacionadas;
* construye una nueva tabla temporal con los resultados.

La base de datos original no se modifica.

El resultado existe únicamente durante la ejecución de la consulta.

---

## Aplicaciones reales

Prácticamente todas las aplicaciones utilizan JOIN constantemente.

Por ejemplo:

* pedidos con el nombre del cliente;
* facturas con los datos del vendedor;
* productos con su categoría;
* matrículas con los datos del estudiante;
* citas médicas con la información del paciente;
* vuelos con el aeropuerto de origen y destino.

Es difícil encontrar una aplicación relacional que no utilice JOIN.

---

## Ideas clave

* El modelo relacional distribuye la información entre varias tablas.
* Los JOIN permiten reconstruir esa información cuando se realiza una consulta.
* La unión se realiza normalmente mediante claves primarias y claves foráneas.
* El resultado del JOIN es una tabla temporal generada durante la ejecución de la consulta.
* Los JOIN constituyen uno de los pilares fundamentales del lenguaje SQL.

