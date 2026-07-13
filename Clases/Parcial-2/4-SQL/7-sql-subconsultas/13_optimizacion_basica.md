# Optimización básica

## Introducción

Las subconsultas son una herramienta muy potente, pero una consulta correcta no siempre es una consulta eficiente.

Cuando el número de registros aumenta hasta cientos de miles o millones de filas, pequeñas diferencias en la forma de escribir una consulta pueden producir mejoras muy importantes en el rendimiento.

El objetivo de este apartado no es estudiar optimización avanzada, sino adquirir una serie de buenas prácticas que nos acompañarán durante todo el curso.

---

## 1. Evitar subconsultas innecesarias

Antes de escribir una subconsulta, pregúntate si realmente es necesaria.

Por ejemplo:

```sql
SELECT
    c.Nombre
FROM Cliente c
WHERE EXISTS
(
    SELECT 1
    FROM Pedido p
    WHERE p.IdCliente = c.IdCliente
);
```

Es una consulta perfectamente razonable.

Sin embargo, en otros casos un `JOIN` puede resultar más sencillo y eficiente.

No existe una regla absoluta; depende del problema.

---

## 2. Cuidado con las subconsultas correlacionadas

Recordemos este ejemplo:

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

Si existen:

* 10 clientes → la subconsulta se ejecutará 10 veces.
* 1.000 clientes → 1.000 veces.
* 1.000.000 clientes → 1.000.000 de veces.

En conjuntos de datos muy grandes, esto puede afectar al rendimiento.

En esos casos conviene estudiar soluciones basadas en `JOIN` y `GROUP BY`.

---

## 3. Crear índices adecuados

Las subconsultas suelen comparar columnas mediante `WHERE`.

Por ejemplo:

```sql
WHERE p.IdCliente = c.IdCliente
```

Si `IdCliente` está indexado, MySQL podrá localizar los registros mucho más rápidamente.

Las claves primarias ya crean índices automáticamente, pero las claves foráneas y otras columnas utilizadas con frecuencia en búsquedas también pueden beneficiarse de índices adicionales.

---

## 4. Seleccionar solo las columnas necesarias

Evita escribir:

```sql
SELECT *
```

si únicamente necesitas:

```sql
SELECT Nombre
```

o

```sql
SELECT Nombre, Precio
```

Cuantas menos columnas recupere la consulta, menos datos deberá procesar y transferir.

---

## 5. Utilizar EXISTS cuando solo interesa la existencia

Muchos estudiantes escriben:

```sql
SELECT COUNT(*)
```

para comprobar si existen registros.

En cambio:

```sql
EXISTS
```

permite que MySQL deje de buscar en cuanto encuentra la primera coincidencia.

En muchos casos resulta una opción más eficiente.

---

## 6. Analizar la legibilidad

Una consulta muy rápida pero imposible de entender puede convertirse en un problema de mantenimiento.

Es preferible escribir consultas ligeramente más largas pero bien estructuradas, con:

* alias descriptivos;
* indentación consistente;
* nombres claros para las columnas calculadas.

El rendimiento también depende de que otros desarrolladores puedan comprender y mantener el código.

---

## 7. Dejar trabajar al optimizador

Las versiones modernas de MySQL incluyen un optimizador muy avanzado.

En muchas ocasiones transformará automáticamente determinadas subconsultas en planes de ejecución equivalentes a un `JOIN`.

Por ello, no conviene obsesionarse con microoptimizaciones prematuras.

Primero debemos escribir una consulta correcta y clara; después, si el rendimiento no es suficiente, analizaremos posibles mejoras.

---

## Recomendaciones finales

Antes de dar por terminada una consulta pregúntate:

* ¿Es correcta?
* ¿Es fácil de leer?
* ¿Devuelve únicamente los datos necesarios?
* ¿Aprovecha los índices existentes?
* ¿Podría simplificarse?

Responder afirmativamente a estas preguntas suele conducir a consultas de buena calidad.

---

## Ideas clave

* Una consulta correcta no siempre es la más eficiente.
* Las subconsultas correlacionadas pueden ser costosas en tablas muy grandes.
* Los índices son fundamentales para acelerar las búsquedas.
* `EXISTS` suele ser preferible a `COUNT()` cuando solo interesa comprobar la existencia de registros.
* La claridad y la mantenibilidad también forman parte de una buena optimización.

