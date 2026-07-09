# SELECT como proyección

## Introducción

Hasta este momento del curso se ha estudiado que el operador de **proyección (π)** permite seleccionar únicamente determinados atributos de una relación. Gracias a este operador es posible eliminar columnas innecesarias y construir nuevas relaciones que contienen únicamente la información relevante para responder a una consulta.

Al comenzar a utilizar SQL, el estudiante descubrirá inmediatamente la cláusula ​**SELECT**​. La similitud entre ambos conceptos no es casual. En realidad, la cláusula SELECT constituye la traducción práctica del operador de proyección del Álgebra Relacional.

Comprender esta equivalencia es mucho más importante que memorizar la sintaxis de SQL. Si un estudiante entiende qué representa una proyección, aprenderá SELECT de forma prácticamente automática.

Durante este capítulo seguiremos utilizando el caso de estudio de la empresa comercial desarrollado a lo largo del curso.

Supongamos la siguiente relación:

| IdCliente | Nombre       | Ciudad    | CorreoElectronico                        | Telefono  |
| ----------: | -------------- | ----------- | ------------------------------------------ | ----------- |
|         1 | Ana Ruiz     | Santander | [ana@empresa.es](mailto:ana@empresa.es)     | 600111111 |
|         2 | Luis Pérez  | Bilbao    | [luis@empresa.es](mailto:luis@empresa.es)   | 600222222 |
|         3 | Marta Gómez | Santander | [marta@empresa.es](mailto:marta@empresa.es) | 600333333 |

Nuestro objetivo será observar cómo una misma consulta puede escribirse tanto mediante Álgebra Relacional como mediante SQL.

### ¿Qué hace realmente una proyección?

Cuando una empresa almacena información de un cliente suele registrar muchos más datos de los que normalmente necesita mostrar.

Por ejemplo, para generar una lista de destinatarios para una campaña comercial únicamente es necesario conocer el nombre y el correo electrónico de cada cliente.

Mostrar también el teléfono, la ciudad o el identificador no aporta ninguna utilidad para esa tarea.

La proyección permite precisamente construir una nueva relación que conserve únicamente los atributos necesarios.

En otras palabras, responde a la pregunta:

> **¿Qué columnas necesito mostrar?**

No responde a qué filas deben aparecer.

Eso será responsabilidad de la selección, que estudiaremos en el siguiente capítulo.

### La proyección en Álgebra Relacional

La notación clásica es:

```text
π Atributo1, Atributo2, ..., AtributoN (Relación)
```

Por ejemplo:

```text
π Nombre, Ciudad (Cliente)
```

El resultado sería:

| Nombre       | Ciudad    |
| -------------- | ----------- |
| Ana Ruiz     | Santander |
| Luis Pérez  | Bilbao    |
| Marta Gómez | Santander |

Obsérvese que la relación original sigue existiendo.

La proyección no modifica los datos almacenados.

Simplemente construye una nueva relación derivada.

### La misma consulta en SQL

La traducción directa es:

```sql
SELECT Nombre, Ciudad
FROM Cliente;
```

Puede observarse que existe una correspondencia prácticamente uno a uno.

| Álgebra Relacional | SQL    |
| --------------------- | -------- |
| π                  | SELECT |
| Relación           | FROM   |

Mientras que el Álgebra Relacional expresa primero la operación y después la relación sobre la que trabaja, SQL separa ambos conceptos mediante las cláusulas SELECT y FROM.

El resultado obtenido es exactamente el mismo.

### SELECT no significa "seleccionar filas"

Uno de los errores más frecuentes durante las primeras clases de SQL consiste en interpretar literalmente el nombre de la cláusula SELECT.

Muchos estudiantes piensan que SELECT sirve para seleccionar registros.

En realidad ocurre lo contrario.

SELECT decide ​**qué columnas aparecerán en el resultado**​.

Las filas que aparecerán dependerán posteriormente de la cláusula WHERE.

Esta diferencia resulta mucho más evidente cuando se conoce previamente el Álgebra Relacional.

| Operación  | Pregunta que responde           |
| ------------- | --------------------------------- |
| π (SELECT) | ¿Qué columnas quiero mostrar? |
| σ (WHERE)  | ¿Qué filas quiero conservar?  |

Comprender esta separación evita una gran cantidad de errores durante el aprendizaje de SQL.

### Eliminación de atributos

Supongamos ahora que únicamente queremos obtener el nombre de todos los clientes.

Álgebra Relacional:

```text
π Nombre (Cliente)
```

SQL:

```sql
SELECT Nombre
FROM Cliente;
```

Obsérvese que desaparecen todos los demás atributos.

No aparecen:

* IdCliente
* Ciudad
* CorreoElectronico
* Telefono

La información no se elimina de la base de datos.

Simplemente deja de formar parte del resultado de la consulta.

### Eliminación de duplicados

Aquí aparece una diferencia importante entre el Álgebra Relacional clásica y SQL.

Supongamos la siguiente relación:

| Ciudad    |
| ----------- |
| Santander |
| Bilbao    |
| Santander |
| Madrid    |
| Bilbao    |

En Álgebra Relacional:

```text
π Ciudad (Cliente)
```

El resultado será:

| Ciudad    |
| ----------- |
| Santander |
| Bilbao    |
| Madrid    |

Las relaciones no pueden contener tuplas duplicadas.

Por tanto, la eliminación de duplicados es automática.

En SQL, sin embargo, ocurre algo diferente.

```sql
SELECT Ciudad
FROM Cliente;
```

El resultado sería:

| Ciudad    |
| ----------- |
| Santander |
| Bilbao    |
| Santander |
| Madrid    |
| Bilbao    |

SQL conserva los duplicados por defecto.

Para obtener el comportamiento del Álgebra Relacional es necesario utilizar:

```sql
SELECT DISTINCT Ciudad
FROM Cliente;
```

Esta es una de las diferencias más importantes entre ambos lenguajes y una de las primeras que todo estudiante debe conocer.

### Casos reales

En una empresa es muy habitual realizar proyecciones para generar informes específicos.

Algunos ejemplos son:

* listado de nombres de clientes;
* catálogo de productos con nombre y precio;
* relación de empleados y departamento;
* inventario con nombre del producto y cantidad disponible.

En todos estos casos la consulta no necesita devolver todos los atributos almacenados.

Reducir el número de columnas mejora la claridad del resultado y disminuye el volumen de datos transmitidos.

### Errores frecuentes

Uno de los errores más comunes consiste en utilizar SELECT \* por comodidad.

Aunque esta práctica resulta aceptable durante las primeras pruebas, en aplicaciones reales suele considerarse una mala práctica.

Solicitar todas las columnas implica:

* mayor consumo de memoria;
* mayor tráfico de datos;
* consultas menos claras;
* mayor dependencia de la estructura de la tabla.

Siempre que sea posible debe solicitarse únicamente la información realmente necesaria.

Otro error frecuente consiste en olvidar que el Álgebra Relacional elimina automáticamente los duplicados mientras que SQL no lo hace.

Este comportamiento será especialmente importante cuando posteriormente se estudien consultas sobre grandes volúmenes de datos.

### Ideas clave

* El operador de proyección (π) corresponde a la cláusula SELECT de SQL.
* La proyección responde a la pregunta ​**"¿qué columnas quiero mostrar?"**​.
* SELECT no decide qué filas aparecen; esa función corresponde a WHERE.
* La proyección construye una nueva relación sin modificar la información almacenada.
* El Álgebra Relacional elimina automáticamente las tuplas duplicadas, mientras que SQL necesita la cláusula DISTINCT para obtener el mismo comportamiento.
* En aplicaciones reales es recomendable evitar `SELECT *` y solicitar únicamente los atributos necesarios.

