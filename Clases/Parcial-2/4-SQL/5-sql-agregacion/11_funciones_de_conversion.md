# Funciones de conversión

## Introducción

En ocasiones los datos almacenados no tienen el tipo adecuado para realizar una determinada operación.

Por ejemplo:

* convertir un número en texto para construir un informe;
* transformar una cadena en una fecha;
* convertir un valor decimal a entero;
* mostrar un número con un formato específico.

Para estos casos MySQL incorpora diversas funciones de conversión.

Estas funciones permiten transformar un dato de un tipo a otro de forma controlada.

---

## CAST()

La función más importante es `CAST()`.

Su sintaxis general es:

```sql
CAST(expresión AS tipo)
```

Permite convertir prácticamente cualquier tipo de dato.

---

## Convertir texto en número

Supongamos que recibimos un valor almacenado como texto.

```sql
SELECT
    CAST('150' AS UNSIGNED) AS Numero;
```

Resultado:

| Numero |
| -------: |
|    150 |

Ahora el valor puede utilizarse en operaciones matemáticas.

---

## Convertir número en texto

También es posible realizar la operación contraria.

```sql
SELECT
    CONCAT(
        'Precio: ',
        CAST(Precio AS CHAR)
    )
FROM Producto;
```

La conversión permite combinar números con cadenas de texto.

---

## Convertir a fecha

Si una fecha ha sido almacenada como texto, puede convertirse.

```sql
SELECT
    CAST(
        '2026-07-13'
        AS DATE
    );
```

Resultado:

| DATE       |
| ------------ |
| 2026-07-13 |

Aunque es posible hacerlo, la mejor práctica consiste en almacenar las fechas correctamente desde el principio.

---

## CONVERT()

MySQL también ofrece la función `CONVERT()`.

```sql
SELECT
    CONVERT(
        Precio,
        CHAR
    )
FROM Producto;
```

En la mayoría de situaciones modernas, `CAST()` resulta más legible y portable entre distintos sistemas gestores de bases de datos.

Por ello será la función recomendada durante este curso.

---

## Conversión implícita

En algunos casos MySQL realiza conversiones automáticamente.

Por ejemplo:

```sql
SELECT
    5 + '10';
```

Resultado:

| Resultado |
| ----------: |
|        15 |

El gestor convierte automáticamente la cadena `'10'` en un número.

Aunque esto pueda parecer cómodo, no es recomendable depender de estas conversiones implícitas.

---

## Riesgos de las conversiones automáticas

Las conversiones implícitas pueden producir resultados inesperados.

```sql
SELECT
    'ABC' + 5;
```

Dependiendo del contexto y de la configuración del servidor, MySQL puede generar advertencias o interpretar el texto como el valor `0`.

Por ello es preferible realizar siempre conversiones explícitas cuando exista cualquier duda.

---

## Aplicaciones reales

Las funciones de conversión son útiles para:

* importar datos desde archivos CSV;
* limpiar información procedente de otras aplicaciones;
* preparar informes;
* combinar texto y números;
* adaptar tipos de datos entre distintas tablas.

---

## Ideas clave

* `CAST()` permite convertir datos entre distintos tipos.
* `CONVERT()` ofrece funcionalidades similares específicas de MySQL.
* Es preferible utilizar conversiones explícitas antes que depender de las conversiones automáticas.
* Un buen diseño de la base de datos reduce la necesidad de realizar conversiones frecuentes.
* Las funciones de conversión son especialmente útiles durante procesos de importación y limpieza de datos.

