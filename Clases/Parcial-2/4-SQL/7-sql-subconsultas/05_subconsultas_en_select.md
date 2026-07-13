# Subconsultas en SELECT

## Introducción

Hasta ahora hemos utilizado subconsultas para:

* obtener un valor (`WHERE`);
* construir tablas temporales (`FROM`).

Existe un tercer lugar donde pueden aparecer:

**la lista de columnas del `SELECT`.**

En este caso, la subconsulta calcula un valor que será mostrado como una columna más del resultado.

Aunque este tipo de consultas suele implicar subconsultas correlacionadas (que veremos en el siguiente apartado), es conveniente comprender primero su funcionamiento básico.

---

## Primer ejemplo

Supongamos que queremos mostrar todos los clientes junto con el número total de pedidos existentes en la base de datos.

```sql
SELECT
    Nombre,
    (
        SELECT COUNT(*)
        FROM Pedido
    ) AS TotalPedidos
FROM Cliente;
```

Resultado:

| Cliente | TotalPedidos |
| --------- | -------------: |
| Ana     |          125 |
| Luis    |          125 |
| Marta   |          125 |

La subconsulta devuelve un único valor y dicho valor aparece repetido en todas las filas.

---

## Otro ejemplo

Podemos mostrar la fecha del último pedido registrado.

```sql
SELECT
    Nombre,
    (
        SELECT MAX(Fecha)
        FROM Pedido
    ) AS UltimoPedido
FROM Cliente;
```

El resultado será similar a:

| Cliente | Último pedido |
| --------- | ---------------- |
| Ana     | 2026-05-20     |
| Luis    | 2026-05-20     |
| Marta   | 2026-05-20     |

La subconsulta se utiliza para enriquecer el resultado de la consulta principal.

---

## Columnas calculadas

Las subconsultas en `SELECT` suelen utilizarse para generar columnas calculadas.

Por ejemplo:

* número total de ventas;
* salario medio;
* precio máximo;
* cantidad de productos;
* fecha más reciente.

Estas columnas pueden combinarse con otras procedentes de las tablas.

---

## ¿Cuándo resultan útiles?

Son especialmente útiles cuando queremos añadir información global a un informe.

Por ejemplo:

| Cliente | Compra | Media empresa |
| --------- | -------- | --------------- |

o

| Producto | Precio | Precio medio |

En ambos casos la subconsulta genera un valor que complementa la información de cada fila.

---

## Limitaciones

Al igual que ocurría en `WHERE`, las subconsultas simples situadas en `SELECT` deben devolver un único valor.

Si devolvieran varias filas, MySQL produciría un error.

Cuando necesitemos que el valor dependa de cada fila concreta aparecerán las ​**subconsultas correlacionadas**​, que estudiaremos a continuación.

---

## Relación con las subconsultas correlacionadas

En la práctica profesional muchas subconsultas situadas en `SELECT` son correlacionadas.

Por ejemplo:

```text
Cliente

↓

Número de pedidos de ese cliente
```

Cada fila produce un resultado diferente.

Este mecanismo constituye uno de los temas más interesantes del SQL avanzado y será el siguiente que estudiaremos.

---

## Ideas clave

* Las subconsultas también pueden aparecer dentro del `SELECT`.
* Su resultado se muestra como una columna más del informe.
* Deben devolver un único valor.
* Son muy útiles para añadir información agregada a los resultados.
* Constituyen la base para comprender las subconsultas correlacionadas.

