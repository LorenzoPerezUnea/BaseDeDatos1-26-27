# CREATE INDEX

## Introducción

Ahora que comprendemos qué es un índice y cómo funciona internamente mediante una estructura B-Tree, ha llegado el momento de aprender a crearlos.

Aunque MySQL genera automáticamente algunos índices —como los asociados a las claves primarias y a muchas restricciones `UNIQUE`—, en la mayoría de los proyectos será el diseñador de la base de datos quien deba crear índices adicionales para mejorar el rendimiento de determinadas consultas.

Saber **cuándo** crear un índice es tan importante como saber **cómo** hacerlo.

En este apartado aprenderemos la sintaxis de `CREATE INDEX`, analizaremos varios ejemplos y veremos cómo comprobar que MySQL realmente está utilizando el índice creado.

## Índices automáticos

Antes de crear nuevos índices conviene recordar que algunos ya existen.

Por ejemplo:

```sql
CREATE TABLE Cliente
(
    IdCliente INT PRIMARY KEY,
    Nombre VARCHAR(100)
);
```

La clave primaria crea automáticamente un índice sobre:

```text
IdCliente
```

No es necesario volver a crearlo manualmente.

Hacerlo supondría únicamente desperdiciar espacio y aumentar el trabajo de mantenimiento.

## Sintaxis básica

La forma más habitual de crear un índice es:

```sql
CREATE INDEX nombre_indice
ON Tabla (Columna);
```

Por ejemplo:

```sql
CREATE INDEX idx_cliente_nombre
ON Cliente (Nombre);
```

A partir de ese momento MySQL podrá utilizar dicho índice cuando resulte conveniente.

## Un ejemplo práctico

Supongamos la siguiente tabla.

```sql
CREATE TABLE Producto
(
    IdProducto INT PRIMARY KEY,
    Nombre VARCHAR(200),
    Precio DECIMAL(10,2),
    Categoria VARCHAR(100)
);
```

La aplicación realiza constantemente consultas como esta:

```sql
SELECT *
FROM Producto
WHERE Categoria = 'Portátiles';
```

Si la tabla contiene cientos de miles de productos, esta consulta puede beneficiarse de un índice.

```sql
CREATE INDEX idx_producto_categoria
ON Producto (Categoria);
```

## Consultar los índices existentes

Podemos comprobar qué índices posee una tabla mediante:

```sql
SHOW INDEX
FROM Producto;
```

El resultado mostrará información como:

- Nombre del índice.
- Columna indexada.
- Tipo.
- Cardinalidad.
- Unicidad.

Esta instrucción resulta muy útil antes de crear nuevos índices para evitar duplicados innecesarios.

## El nombre del índice

Aunque MySQL permite utilizar prácticamente cualquier identificador válido, es recomendable seguir una convención.

Por ejemplo:

```text
idx_cliente_nombre
```

```text
idx_producto_categoria
```

```text
idx_pedido_fecha
```

El prefijo `idx_` facilita identificar rápidamente que se trata de un índice.

En proyectos grandes esta práctica mejora considerablemente la legibilidad.

## Índices sobre varias columnas

También es posible crear índices que incluyan varias columnas.

```sql
CREATE INDEX idx_cliente_ciudad_nombre
ON Cliente
(
    Ciudad,
    Nombre
);
```

Estos índices, conocidos como **índices compuestos**, se estudiarán con detalle en el siguiente apartado.

## Eliminar un índice

Si un índice deja de ser útil, puede eliminarse mediante:

```sql
DROP INDEX idx_producto_categoria
ON Producto;
```

Eliminar índices innecesarios reduce el espacio ocupado y mejora el rendimiento de las operaciones de escritura.

## ¿Cuándo conviene crear un índice?

Generalmente cuando una columna aparece con frecuencia en consultas como:

```sql
SELECT *
FROM Cliente
WHERE Apellidos = 'García';
```

o bien:

```sql
SELECT *
FROM Pedido
WHERE FechaPedido >= '2026-01-01';
```

También suele ser recomendable en columnas utilizadas para relacionar tablas mediante `JOIN`.

## ¿Cuándo no merece la pena?

Crear un índice sobre una columna apenas utilizada no aportará beneficios.

Por ejemplo, si una columna solo aparece en informes anuales, el coste de mantener el índice puede ser superior a la mejora obtenida.

Del mismo modo, no suele compensar indexar columnas con muy pocos valores distintos, como un campo que únicamente pueda contener:

```text
Sí

No
```

En estos casos el optimizador puede preferir recorrer directamente la tabla.

## Verificando el resultado

Después de crear un índice no debemos asumir que MySQL lo utilizará siempre.

La herramienta adecuada para comprobarlo será:

```sql
EXPLAIN
```

que estudiaremos en próximos apartados.

Es el plan de ejecución, y no la existencia del índice por sí sola, el que determina si realmente se está aprovechando.

## Buenas prácticas

- Crear índices únicamente cuando exista una necesidad demostrable.
- Utilizar nombres descriptivos y consistentes.
- Revisar los índices ya existentes antes de crear otros nuevos.
- Eliminar índices que hayan dejado de utilizarse.
- Verificar siempre su uso mediante `EXPLAIN`.

## Conclusiones

`CREATE INDEX` permite añadir estructuras auxiliares que aceleran el acceso a los datos sin modificar la información almacenada. Sin embargo, cada índice introduce un coste de mantenimiento, por lo que su creación debe responder a necesidades reales de las consultas más frecuentes.

## Ideas clave

- `CREATE INDEX` crea un índice sobre una o varias columnas.
- Las claves primarias ya generan un índice automáticamente.
- Los índices deben tener nombres descriptivos.
- Es posible consultar los índices existentes con `SHOW INDEX`.
- La utilidad de un índice debe comprobarse mediante el plan de ejecución y no únicamente por su existencia.

