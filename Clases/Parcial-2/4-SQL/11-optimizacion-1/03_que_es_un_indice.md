# ¿Qué es un índice?

## Introducción

Uno de los conceptos más importantes relacionados con el rendimiento de una base de datos es el **índice**.

De hecho, la inmensa mayoría de las optimizaciones realizadas sobre bases de datos relacionales comienzan precisamente por un buen diseño de índices.

Un índice es una estructura de datos adicional que permite localizar registros mucho más rápidamente que realizando un recorrido completo de la tabla.

Su objetivo principal no es almacenar información nueva, sino facilitar el acceso a la información ya existente.

Sin índices, muchas consultas sobre bases de datos de gran tamaño resultarían demasiado lentas para ser utilizadas en aplicaciones reales.

## Una analogía

Imaginemos un libro de mil páginas.

Queremos localizar el capítulo dedicado a las transacciones.

Tenemos dos posibilidades.

La primera consiste en leer todas las páginas desde el principio hasta encontrar el capítulo.

La segunda consiste en consultar el índice situado al comienzo del libro.

Gracias al índice sabemos inmediatamente que el capítulo comienza, por ejemplo, en la página 325.

El índice evita recorrer innecesariamente las páginas anteriores.

Los índices de una base de datos cumplen exactamente la misma función.

## ¿Qué problema resuelve?

Supongamos una tabla con diez millones de clientes.

```text
Cliente

10 000 000 registros
```

Buscamos uno concreto.

```sql
SELECT *
FROM Cliente
WHERE IdCliente = 7845123;
```

Si no existiera ningún índice, MySQL tendría que revisar los registros uno por uno hasta localizar el cliente solicitado.

En el peor caso leería los diez millones de registros.

Con un índice, el motor puede localizar directamente la posición aproximada del registro sin recorrer toda la tabla.

## ¿Dónde se almacena un índice?

Un índice no sustituye a la tabla.

Es una estructura independiente mantenida automáticamente por el SGBD.

Conceptualmente podemos imaginar algo parecido a esto.

```text
Tabla Cliente

↓

Registro 1

Registro 2

Registro 3

...

Registro N
```

Además existe otra estructura.

```text
Índice

↓

Valor

↓

Posición del registro
```

Cuando buscamos un determinado valor, MySQL consulta primero el índice y después accede únicamente a los registros necesarios.

## Ejemplo

Supongamos la siguiente tabla.

```sql
CREATE TABLE Cliente (

    IdCliente INT PRIMARY KEY,

    Nombre VARCHAR(100),

    Ciudad VARCHAR(100)

);
```

La clave primaria genera automáticamente un índice.

Consulta.

```sql
SELECT *
FROM Cliente
WHERE IdCliente = 3500;
```

El optimizador utilizará normalmente ese índice para localizar el registro.

En cambio:

```sql
SELECT *
FROM Cliente
WHERE Ciudad = 'Sevilla';
```

Si la columna `Ciudad` no dispone de un índice, probablemente será necesario recorrer toda la tabla.

## ¿Qué contiene realmente un índice?

De forma simplificada, un índice almacena:

- El valor indexado.
- Una referencia al registro correspondiente.

Por ejemplo.

```text
15 → Registro 128

18 → Registro 654

20 → Registro 981

24 → Registro 1420
```

Cuando buscamos el valor:

```
20
```

MySQL no necesita revisar todos los registros.

Accede directamente a la posición indicada por el índice.

## Ventajas

Los índices ofrecen numerosas ventajas.

Entre ellas:

- Aceleran búsquedas mediante `WHERE`.
- Mejoran muchos `JOIN`.
- Facilitan las ordenaciones (`ORDER BY`).
- Mejoran determinados `GROUP BY`.
- Reducen el número de páginas leídas desde disco.
- Disminuyen el tiempo de respuesta de numerosas consultas.

Por este motivo son una de las herramientas más importantes para optimizar bases de datos.

## ¿Tienen inconvenientes?

Sí.

Un error frecuente consiste en pensar que cuántos más índices tenga una tabla, mejor será su rendimiento.

En realidad ocurre lo contrario.

Cada índice adicional implica:

- Más espacio ocupado en disco.
- Mayor consumo de memoria.
- Mayor tiempo durante los `INSERT`.
- Mayor tiempo durante los `UPDATE`.
- Mayor tiempo durante los `DELETE`.

Cada vez que cambia un registro, todos los índices afectados deben actualizarse.

Por ello únicamente deben crearse cuando realmente aportan beneficios.

## ¿Qué columnas suelen indexarse?

Normalmente conviene indexar columnas utilizadas con frecuencia en:

```sql
WHERE
```

```sql
JOIN
```

```sql
ORDER BY
```

```sql
GROUP BY
```

No obstante, la decisión depende del patrón real de uso de la aplicación.

## ¿Qué columnas suelen evitarse?

En general no suele ser recomendable crear índices sobre columnas que:

- Contienen muy pocos valores distintos.
- Cambian continuamente.
- Apenas se utilizan en consultas.
- Contienen textos muy largos.

En apartados posteriores estudiaremos estos casos con mayor detalle.

## Buenas prácticas

- Crear índices únicamente cuando exista una necesidad real.
- Analizar previamente las consultas más utilizadas.
- Aprovechar los índices creados automáticamente por claves primarias y únicas.
- Revisar periódicamente los índices existentes.
- Medir siempre el efecto de un nuevo índice sobre el rendimiento.

## Conclusiones

Los índices constituyen una de las herramientas más eficaces para mejorar el rendimiento de una base de datos relacional. Permiten localizar registros de forma mucho más eficiente que un recorrido completo de la tabla, aunque también introducen costes de almacenamiento y mantenimiento que deben tenerse en cuenta durante el diseño.

## Ideas clave

- Un índice es una estructura auxiliar que acelera el acceso a los datos.
- No almacena información nueva, sino referencias a los registros existentes.
- Reduce el número de lecturas necesarias para localizar información.
- También tiene costes de mantenimiento.
- Un buen diseño de índices puede mejorar drásticamente el rendimiento de una aplicación.

