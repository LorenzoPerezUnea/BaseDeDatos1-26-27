# ¿Por qué una consulta es lenta?

## Introducción

Uno de los errores más comunes entre los estudiantes que comienzan a trabajar con bases de datos consiste en pensar que todas las consultas SQL tienen un coste similar.

Desde el punto de vista del lenguaje SQL esto parece razonable.

Dos consultas pueden tener prácticamente la misma sintaxis:

```sql
SELECT *
FROM Cliente
WHERE IdCliente = 125;
```

y

```sql
SELECT *
FROM Cliente
WHERE Nombre = 'Juan';
```

Ambas parecen igual de sencillas.

Sin embargo, una puede ejecutarse en menos de un milisegundo mientras que la otra tarda varios segundos.

¿Por qué ocurre esto?

La respuesta se encuentra en la forma en que MySQL localiza la información dentro de la base de datos.

Comprender este proceso es el primer paso para aprender a optimizar consultas.

## ¿Qué significa que una consulta sea lenta?

Cuando hablamos del rendimiento de una consulta normalmente nos referimos al tiempo que necesita para completarse.

Este tiempo depende de numerosos factores, entre ellos:

- Número de registros.
- Cantidad de tablas implicadas.
- Existencia de índices.
- Tipo de almacenamiento.
- Cantidad de memoria disponible.
- Velocidad del disco.
- Número de usuarios concurrentes.
- Complejidad del plan de ejecución.

No todas las consultas consumen los mismos recursos.

## El tamaño de los datos importa

Supongamos una tabla muy pequeña.

```text
Cliente

10 registros
```

Buscar un cliente concreto resulta prácticamente instantáneo.

Ahora imaginemos esa misma tabla varios años después.

```text
Cliente

15 000 000 registros
```

Si MySQL tuviera que revisar uno por uno todos los registros hasta encontrar el cliente buscado, el tiempo de respuesta aumentaría considerablemente.

Este proceso recibe el nombre de **escaneo completo de tabla** (*Full Table Scan*).

## Escaneo completo

Cuando no existe un mecanismo que permita localizar rápidamente un registro, el motor no tiene otra alternativa que leer toda la tabla.

Conceptualmente realiza un proceso similar al siguiente.

```text
Registro 1

↓

Registro 2

↓

Registro 3

↓

...

↓

Registro 15 000 000
```

En el peor caso deberá leer absolutamente todos los registros.

Este comportamiento puede resultar aceptable para tablas pequeñas, pero se convierte en un problema serio cuando el volumen de información crece.

## Una analogía

Imaginemos que deseamos encontrar una palabra en un diccionario.

Existen dos posibilidades.

La primera consiste en abrir el libro por la primera página y leer palabra por palabra hasta encontrar la buscada.

La segunda consiste en utilizar el orden alfabético del diccionario.

La diferencia entre ambos métodos es enorme.

Los índices funcionan precisamente como ese orden alfabético.

Permiten localizar información sin recorrer todos los registros.

## Factores que influyen en el rendimiento

Aunque los índices desempeñan un papel fundamental, no son el único factor.

También influyen aspectos como:

### Número de filas

Cuantos más registros existan, mayor será el trabajo necesario para procesarlos.

### Número de columnas

Leer filas muy anchas implica mover más información entre el disco y la memoria.

### Filtros utilizados

No es lo mismo recuperar toda una tabla que únicamente un pequeño subconjunto de registros.

Por ejemplo:

```sql
SELECT *
FROM Pedido;
```

frente a:

```sql
SELECT *
FROM Pedido
WHERE IdPedido = 350;
```

### Ordenaciones

Cuando utilizamos:

```sql
ORDER BY
```

MySQL puede necesitar ordenar millones de registros antes de devolver el resultado.

Si existe un índice adecuado, muchas veces podrá evitar ese trabajo.

### Agrupaciones

Operaciones como:

```sql
GROUP BY
```

requieren clasificar registros y calcular agregaciones.

Dependiendo del volumen de datos, pueden convertirse en operaciones costosas.

### JOIN

Cada tabla adicional implica nuevas operaciones de búsqueda y combinación.

Una consulta que une cinco tablas suele ser mucho más compleja que otra que consulta una sola.

## El hardware también influye

Dos servidores ejecutando exactamente la misma consulta pueden obtener tiempos distintos.

Algunos factores físicos son:

- Memoria RAM.
- Tipo de disco (SSD o HDD).
- Número de núcleos del procesador.
- Caché disponible.
- Velocidad del sistema de almacenamiento.

Sin embargo, incluso utilizando un hardware muy potente, una consulta mal diseñada seguirá siendo ineficiente.

La optimización comienza siempre por el diseño de la consulta y de la base de datos.

## Un ejemplo

Supongamos una tabla con diez millones de clientes.

Consulta A.

```sql
SELECT *
FROM Cliente
WHERE IdCliente = 1500000;
```

Consulta B.

```sql
SELECT *
FROM Cliente
WHERE Ciudad = 'Madrid';
```

Aunque ambas parecen similares, probablemente la primera sea mucho más rápida porque la clave primaria suele estar indexada automáticamente.

La segunda dependerá de si existe o no un índice sobre la columna `Ciudad`.

## ¿Cómo sabe MySQL qué hacer?

Cuando enviamos una consulta SQL, MySQL no comienza inmediatamente a leer datos.

Antes realiza un proceso interno de análisis.

Entre otras tareas:

- Comprueba la sintaxis.
- Analiza las tablas implicadas.
- Estudia los índices disponibles.
- Calcula distintos planes de ejecución.
- Estima el coste de cada alternativa.
- Selecciona la estrategia más eficiente.

Todo este trabajo lo realiza un componente denominado **optimizador de consultas**, que estudiaremos en el siguiente apartado.

## Buenas prácticas

- No asumir que una consulta sencilla será necesariamente rápida.
- Diseñar tablas pensando en el volumen real de datos.
- Evitar leer información innecesaria.
- Analizar siempre las consultas críticas.
- Medir el rendimiento antes y después de realizar cambios.

## Conclusiones

El rendimiento de una consulta depende de mucho más que de su sintaxis. El tamaño de las tablas, la existencia de índices, el tipo de operaciones realizadas y las decisiones tomadas por el optimizador influyen directamente en el tiempo de ejecución. Comprender estos factores constituye el primer paso para aprender a optimizar bases de datos de forma profesional.

## Ideas clave

- Una consulta correcta no siempre es una consulta eficiente.
- El volumen de datos condiciona el rendimiento.
- Los escaneos completos de tabla suelen ser costosos.
- Los índices permiten localizar registros mucho más rápidamente.
- El optimizador de MySQL decide cómo ejecutar cada consulta.

