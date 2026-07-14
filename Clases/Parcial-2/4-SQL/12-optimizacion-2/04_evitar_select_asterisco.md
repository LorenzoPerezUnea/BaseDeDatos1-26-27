# Evitar SELECT *

## Introducción

Una de las primeras instrucciones que aprende cualquier estudiante de SQL es:

```sql
SELECT *
FROM Tabla;
```

El carácter `*` indica que deben recuperarse **todas las columnas** de la tabla.

Durante el aprendizaje resulta muy cómodo porque evita escribir el nombre de cada columna.

Sin embargo, en aplicaciones profesionales el uso indiscriminado de `SELECT *` se considera una mala práctica en la mayoría de los casos.

No significa que esté prohibido.

Existen situaciones donde resulta perfectamente válido.

El problema aparece cuando se convierte en un hábito.

## ¿Qué hace realmente SELECT *?

Supongamos la siguiente tabla.

```text
Producto
```

Contiene las siguientes columnas:

```text
IdProducto

Nombre

Descripcion

Precio

Stock

Peso

Categoria

Proveedor

FechaAlta

Activo
```

La consulta:

```sql
SELECT *
FROM Producto;
```

devuelve absolutamente todas ellas.

Aunque la aplicación únicamente necesite mostrar:

- Nombre.
- Precio.

MySQL recuperará igualmente el resto de la información.

## ¿Por qué puede ser un problema?

Cuantas más columnas se recuperan:

- Mayor cantidad de datos debe leer MySQL.
- Más información debe enviarse por la red.
- Más memoria consume la aplicación.
- Mayor tiempo requiere el procesamiento.

En tablas pequeñas la diferencia suele ser insignificante.

En tablas con millones de registros puede convertirse en un problema importante.

## Un ejemplo práctico

Supongamos una tabla con:

- 5 millones de productos.
- 20 columnas.
- Una columna `Descripcion` de varios miles de caracteres.

La aplicación únicamente necesita mostrar:

- Nombre.
- Precio.

Consulta poco recomendable.

```sql
SELECT *
FROM Producto;
```

Consulta recomendable.

```sql
SELECT
    Nombre,
    Precio
FROM Producto;
```

La segunda consulta transfiere una cantidad muchísimo menor de información.

## Cambios futuros en la tabla

Otro inconveniente importante aparece cuando el esquema evoluciona.

Supongamos que inicialmente la tabla contiene:

```text
Nombre

Precio
```

y la aplicación utiliza:

```sql
SELECT *
```

Meses después se añade una nueva columna.

```text
ImagenAltaResolucion
```

A partir de ese momento todas las consultas comenzarán a recuperar también esa información, aunque la aplicación nunca la utilice.

El consumo de recursos aumentará sin que ningún desarrollador haya modificado el código SQL.

## Dependencia del orden de las columnas

Algunas aplicaciones procesan los resultados por posición.

Por ejemplo:

```text
Columna 1

Columna 2

Columna 3
```

Si posteriormente se modifica el orden de las columnas de la tabla, el comportamiento puede cambiar inesperadamente.

Cuando se indican explícitamente los nombres:

```sql
SELECT
    Nombre,
    Precio
```

el resultado permanece estable.

## Índices de cobertura

Existe otro aspecto relacionado con el rendimiento.

Supongamos un índice sobre:

```text
Categoria

Precio
```

Consulta.

```sql
SELECT
    Categoria,
    Precio
FROM Producto
WHERE Categoria = 'Monitores';
```

Toda la información necesaria se encuentra ya dentro del índice.

En muchos casos MySQL puede responder sin acceder a la tabla.

Esto recibe el nombre de **índice de cobertura** (*Covering Index*).

Sin embargo, si escribimos:

```sql
SELECT *
```

el motor necesitará acceder a la tabla para obtener las columnas restantes.

Se pierde una posible optimización.

## ¿Cuándo sí puede utilizarse?

Existen situaciones donde `SELECT *` resulta razonable.

Por ejemplo:

Durante el aprendizaje.

```sql
SELECT *
FROM Cliente;
```

Para explorar una tabla desconocida.

En consultas rápidas realizadas desde herramientas administrativas.

Durante pruebas o depuración.

En estos casos la comodidad suele ser más importante que la optimización.

## ¿Cuándo conviene evitarlo?

Especialmente en:

- Aplicaciones web.
- Sistemas empresariales.
- APIs.
- Informes periódicos.
- Consultas muy frecuentes.
- Tablas con muchas columnas.
- Tablas con columnas de gran tamaño.

## Una buena costumbre

Antes de escribir una consulta conviene preguntarse:

> ¿Qué columnas necesita realmente mi aplicación?

Si únicamente son tres, deben seleccionarse únicamente esas tres.

Esta sencilla práctica mejora tanto el rendimiento como la claridad del código.

## Buenas prácticas

- Especificar siempre las columnas necesarias.
- Evitar recuperar información que no vaya a utilizarse.
- Aprovechar índices de cobertura cuando sea posible.
- Utilizar `SELECT *` únicamente durante pruebas o exploración de datos.
- Revisar consultas antiguas que utilicen `SELECT *` de forma sistemática.

## Conclusiones

`SELECT *` resulta muy útil durante el aprendizaje y en determinadas tareas administrativas, pero en aplicaciones profesionales suele ser preferible seleccionar únicamente las columnas necesarias. Esta práctica reduce el consumo de recursos, mejora la legibilidad y permite aprovechar determinadas optimizaciones del motor de base de datos.

## Ideas clave

- `SELECT *` recupera todas las columnas de una tabla.
- Normalmente la aplicación solo necesita una parte de esa información.
- Recuperar menos columnas reduce el trabajo realizado por MySQL.
- Puede impedir el uso de índices de cobertura.
- Seleccionar explícitamente las columnas mejora el mantenimiento del código.

