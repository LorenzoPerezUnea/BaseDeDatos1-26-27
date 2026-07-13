# DISTINCT

## Introducción

En muchas ocasiones una tabla contiene valores repetidos.

Por ejemplo, varios clientes pueden vivir en la misma ciudad, distintos empleados pueden ocupar el mismo cargo o numerosos productos pueden pertenecer a la misma categoría.

Cuando realizamos una consulta normal, SQL devuelve ​**todas las filas**​, incluso aunque algunos valores estén repetidos.

Sin embargo, existen situaciones en las que únicamente nos interesa conocer los valores diferentes.

Para ello utilizaremos la palabra reservada ​**`DISTINCT`**​.

Esta operación corresponde directamente al concepto de eliminación de duplicados en el resultado de una consulta y constituye una herramienta muy utilizada para generar listados únicos.

---

## Consulta sin DISTINCT

Supongamos la siguiente información.

| IdCliente | Nombre | Ciudad    |
| ----------: | -------- | ----------- |
|         1 | Ana    | Santander |
|         2 | Luis   | Bilbao    |
|         3 | Marta  | Santander |
|         4 | Javier | Burgos    |
|         5 | Elena  | Bilbao    |

Si ejecutamos:

```sql
SELECT Ciudad
FROM Cliente;
```

obtendremos:

| Ciudad    |
| ----------- |
| Santander |
| Bilbao    |
| Santander |
| Burgos    |
| Bilbao    |

Observamos que aparecen ciudades repetidas.

---

## Utilizando DISTINCT

Si únicamente queremos conocer las ciudades existentes utilizamos:

```sql
SELECT DISTINCT Ciudad
FROM Cliente;
```

Resultado:

| Ciudad    |
| ----------- |
| Santander |
| Bilbao    |
| Burgos    |

Ahora cada ciudad aparece una sola vez.

---

## DISTINCT sobre varias columnas

`DISTINCT` también puede aplicarse sobre varias columnas simultáneamente.

```sql
SELECT DISTINCT
    Ciudad,
    Activo
FROM Cliente;
```

En este caso SQL elimina únicamente aquellas filas en las que **todas las columnas seleccionadas** sean iguales.

No analiza cada columna por separado, sino la combinación completa.

---

## Casos de uso

`DISTINCT` resulta especialmente útil para:

* obtener ciudades donde existen clientes;
* listar cargos diferentes de los empleados;
* conocer las categorías utilizadas;
* identificar estados posibles de un proceso;
* preparar filtros en una aplicación.

Es una operación muy frecuente en sistemas de información y cuadros de mando.

---

## DISTINCT y SELECT \*

Una duda habitual consiste en escribir:

```sql
SELECT DISTINCT *
FROM Cliente;
```

Esta consulta elimina únicamente las filas completamente idénticas.

Como normalmente la clave primaria hace que cada registro sea diferente, esta consulta rara vez resulta útil.

En la mayoría de los casos `DISTINCT` debe aplicarse únicamente sobre las columnas que realmente queremos analizar.

---

## Buenas prácticas

Antes de utilizar `DISTINCT` conviene preguntarse:

> ¿Necesito realmente eliminar duplicados o quiero ver todos los registros?

Muchos estudiantes utilizan `DISTINCT` para ocultar errores en sus consultas.

Lo correcto es comprender por qué aparecen registros repetidos y utilizar `DISTINCT` únicamente cuando el objetivo sea obtener valores únicos.

---

## Ideas clave

* `DISTINCT` elimina valores repetidos del resultado.
* No modifica la información almacenada en la base de datos.
* Puede aplicarse sobre una o varias columnas.
* Es muy útil para generar listados únicos.
* No debe utilizarse como solución a consultas incorrectas.

