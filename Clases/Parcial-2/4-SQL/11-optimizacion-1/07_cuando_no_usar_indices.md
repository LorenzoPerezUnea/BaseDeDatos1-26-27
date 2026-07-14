# Cuándo no usar índices

## Introducción

Hasta este momento podría parecer que los índices son siempre beneficiosos.

Después de todo, aceleran las consultas y permiten localizar registros mucho más rápidamente.

Sin embargo, esta idea es incorrecta.

Uno de los errores más frecuentes entre los desarrolladores con poca experiencia consiste en crear índices sobre casi todas las columnas de una tabla.

Aunque la intención sea mejorar el rendimiento, el resultado suele ser el contrario.

Cada índice ocupa espacio, consume memoria y debe mantenerse actualizado cada vez que cambian los datos.

Por este motivo, un buen diseñador de bases de datos sabe tanto **cuándo crear un índice** como **cuándo evitarlo**.

## Los índices tienen un coste

Cada índice constituye una estructura adicional.

Eso significa que, además de almacenar la tabla, MySQL debe mantener todos los índices asociados.

Cuando ejecutamos:

```sql
INSERT
```

no solo se inserta una fila.

También se actualizan todos los índices afectados.

Lo mismo ocurre con:

```sql
UPDATE
```

y

```sql
DELETE
```

Cuantos más índices existan, mayor será el trabajo necesario para mantenerlos.

## Columnas con pocos valores distintos

Uno de los peores candidatos para crear un índice es una columna con muy poca variedad de valores.

Por ejemplo:

```text
Activo

Sí

No
```

O bien:

```text
Sexo

Hombre

Mujer
```

O incluso:

```text
Estado

Pendiente

Enviado

Cancelado
```

Si prácticamente la mitad de los registros contienen el mismo valor, el índice apenas ayuda a localizar información.

En muchas ocasiones el optimizador prefiere recorrer directamente toda la tabla.

## Columnas que cambian constantemente

Supongamos una tabla de almacén.

```sql
Producto
```

El campo:

```text
Stock
```

puede actualizarse cientos de veces al día.

Si además posee un índice, cada modificación obligará a reorganizar también el árbol correspondiente.

En este tipo de situaciones el coste del mantenimiento puede superar el beneficio obtenido en las consultas.

## Tablas muy pequeñas

Cuando una tabla contiene únicamente unas pocas decenas de registros, utilizar un índice apenas aporta ventajas.

Por ejemplo:

```text
País

25 registros
```

o

```text
TiposIVA

5 registros
```

En estos casos leer toda la tabla resulta tan rápido que el índice no ofrece una mejora apreciable.

## Columnas que nunca aparecen en consultas

Si una columna no participa en:

- `WHERE`
- `JOIN`
- `ORDER BY`
- `GROUP BY`

difícilmente un índice aportará beneficios.

Crear índices "por si acaso" suele terminar generando un sistema más lento y con mayor consumo de almacenamiento.

## Índices duplicados

Supongamos que existe:

```sql
PRIMARY KEY (IdCliente)
```

Crear además:

```sql
CREATE INDEX idx_idcliente
ON Cliente(IdCliente);
```

carece completamente de sentido.

La clave primaria ya dispone de un índice.

Mantener otro idéntico solo incrementa el espacio ocupado y el trabajo durante las operaciones de escritura.

## Demasiados índices

Cada índice adicional aumenta:

- El tiempo de inserción.
- El tiempo de actualización.
- El tiempo de eliminación.
- El espacio ocupado en disco.
- El uso de memoria.

Una tabla con veinte índices puede ofrecer un excelente rendimiento en consultas, pero un comportamiento muy pobre cuando se insertan miles de registros por segundo.

Por ello debe buscarse un equilibrio entre lectura y escritura.

## Índices sobre columnas muy largas

Columnas como:

```text
Descripción
```

o

```text
Observaciones
```

que contienen textos extensos no suelen ser buenas candidatas para índices B-Tree convencionales.

En búsquedas de texto libre suelen utilizarse otras técnicas, como índices de texto completo (*FULLTEXT*), que estudiaremos en clases posteriores.

## Índices que nunca utiliza el optimizador

No basta con crear un índice.

Es necesario comprobar que realmente se utiliza.

Puede ocurrir que una consulta siga realizando un escaneo completo de la tabla porque el optimizador considera que el índice no resulta rentable.

Por ello siempre es recomendable utilizar:

```sql
EXPLAIN
```

para verificar el comportamiento real de las consultas.

## Buenas prácticas

- Crear índices únicamente cuando exista una necesidad demostrada.
- Evitar indexar columnas con muy baja selectividad.
- Revisar periódicamente los índices que ya no se utilizan.
- Analizar el impacto sobre las operaciones de escritura.
- Medir siempre antes y después de añadir un nuevo índice.

## Conclusiones

Los índices son una herramienta extraordinariamente útil, pero también tienen un coste. Un exceso de índices puede ralentizar las operaciones de inserción, actualización y eliminación, además de consumir espacio adicional. Diseñar una estrategia de indexación adecuada implica encontrar el equilibrio entre rendimiento en lectura y coste de mantenimiento.

## Ideas clave

- Los índices no siempre mejoran el rendimiento.
- Cada índice debe mantenerse actualizado.
- No conviene indexar columnas con pocos valores distintos.
- Las tablas pequeñas rara vez necesitan índices adicionales.
- Un buen diseño prioriza la utilidad real frente a la cantidad de índices.

