# INSERT múltiple

## Introducción

Durante el apartado anterior aprendimos a insertar un único registro mediante `INSERT`.

Sin embargo, en muchas ocasiones necesitamos incorporar decenas, cientos o incluso miles de filas.

Ejecutar una sentencia independiente para cada registro sería poco eficiente y haría el código innecesariamente largo.

Para resolver este problema SQL permite insertar varios registros mediante una única instrucción.

Esta técnica recibe el nombre de ​**inserción múltiple**​.

---

## Sintaxis

La diferencia respecto al `INSERT` básico es muy pequeña.

Después de la palabra `VALUES` simplemente añadimos varios conjuntos de valores separados por comas.

```sql
INSERT INTO NombreTabla
(
    Columna1,
    Columna2
)
VALUES
(
    Valor1,
    Valor2
),
(
    Valor3,
    Valor4
),
(
    Valor5,
    Valor6
);
```

Cada conjunto de paréntesis representa una nueva fila.

---

## Ejemplo con categorías

Poblemos la tabla `Categoria`.

```sql
INSERT INTO Categoria
(
    Nombre,
    Descripcion
)
VALUES
(
    'Portátiles',
    'Ordenadores portátiles'
),
(
    'Monitores',
    'Pantallas y monitores'
),
(
    'Periféricos',
    'Teclados, ratones y accesorios'
),
(
    'Almacenamiento',
    'Discos SSD y HDD'
);
```

Con una única instrucción hemos creado cuatro registros.

---

## Comprobando el resultado

Verificamos la información.

```sql
SELECT *
FROM Categoria;
```

Resultado aproximado.

| IdCategoria | Nombre         |
| ------------: | ---------------- |
|           1 | Portátiles    |
|           2 | Monitores      |
|           3 | Periféricos   |
|           4 | Almacenamiento |

Los identificadores continúan siendo generados automáticamente mediante `AUTO_INCREMENT`.

---

## Ventajas

La inserción múltiple presenta varias ventajas.

* El código ocupa menos espacio.
* Se reduce el número de comunicaciones con el servidor.
* La ejecución suele ser más rápida.
* Resulta especialmente útil durante la carga inicial de una base de datos.

Por este motivo es una técnica ampliamente utilizada en scripts de instalación y migración.

---

## ¿Cuándo utilizarla?

Durante este curso la emplearemos principalmente para poblar el caso práctico.

Por ejemplo:

* categorías;
* empleados;
* productos;
* clientes de prueba.

Más adelante veremos que incluso es posible importar miles de registros utilizando herramientas especializadas, pero conceptualmente todas ellas terminan generando instrucciones similares a este tipo de `INSERT`.

---

## Errores frecuentes

Uno de los errores más habituales consiste en olvidar la coma que separa dos registros consecutivos.

También es frecuente proporcionar un número distinto de valores en alguno de los grupos de paréntesis.

Cada fila debe contener exactamente el mismo número de valores que columnas hemos indicado al principio de la sentencia.

## Ideas clave

* Una única sentencia `INSERT` puede crear varios registros.
* Cada grupo de valores representa una fila distinta.
* La inserción múltiple es más eficiente que ejecutar numerosos `INSERT` individuales.
* Es especialmente útil durante la carga inicial de datos.
* Será la técnica que utilizaremos para poblar gran parte del caso práctico.

