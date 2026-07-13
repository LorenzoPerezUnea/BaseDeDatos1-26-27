# Funciones de cadena

## Introducción

Hasta ahora hemos utilizado funciones de agregación para resumir información.

Sin embargo, SQL incorpora muchos otros tipos de funciones que trabajan ​**sobre cada fila individualmente**​, modificando o transformando el contenido de una columna.

Las primeras que estudiaremos son las ​**funciones de cadena**​, utilizadas para manipular texto.

Estas funciones aparecen constantemente en aplicaciones empresariales para:

* dar formato a nombres;
* construir informes;
* limpiar datos importados;
* generar identificadores;
* preparar información para búsquedas.

A diferencia de `COUNT()` o `SUM()`, estas funciones ​**no agrupan registros**​, sino que procesan cada fila de forma independiente.

---

## LOWER() y UPPER()

Permiten convertir el texto a minúsculas o mayúsculas.

Supongamos la siguiente tabla.

| Nombre      |
| ------------- |
| Ana Ruiz    |
| Luis Gómez |
| Marta Díaz |

Convertir todos los nombres a mayúsculas.

```sql
SELECT
    UPPER(Nombre) AS NombreMayusculas
FROM Cliente;
```

Resultado:

| NombreMayusculas |
| ------------------ |
| ANA RUIZ         |
| LUIS GÓMEZ      |
| MARTA DÍAZ      |

Del mismo modo:

```sql
SELECT
    LOWER(Nombre) AS NombreMinusculas
FROM Cliente;
```

produce:

| NombreMinusculas |
| ------------------ |
| ana ruiz         |
| luis gómez      |
| marta díaz      |

Estas funciones son muy utilizadas para realizar comparaciones sin distinguir entre mayúsculas y minúsculas.

---

## LENGTH()

Devuelve el número de caracteres de una cadena.

```sql
SELECT
    Nombre,
    LENGTH(Nombre) AS Longitud
FROM Cliente;
```

Resultado:

| Nombre      | Longitud |
| ------------- | ---------: |
| Ana Ruiz    |        8 |
| Luis Gómez |       11 |
| Marta Díaz |       11 |

Puede utilizarse para validar datos o detectar registros incorrectos.

---

## CONCAT()

Permite unir varias cadenas.

Supongamos una tabla con:

| Nombre | Apellido |
| -------- | ---------- |
| Ana    | Ruiz     |
| Luis   | Gómez   |

Podemos construir el nombre completo.

```sql
SELECT
    CONCAT(Nombre, ' ', Apellido) AS NombreCompleto
FROM Cliente;
```

Resultado:

| NombreCompleto |
| ---------------- |
| Ana Ruiz       |
| Luis Gómez    |

Es una de las funciones más utilizadas en aplicaciones web.

---

## LEFT() y RIGHT()

Extraen caracteres desde el inicio o el final de una cadena.

```sql
SELECT
    LEFT(Nombre,3) AS Inicio
FROM Cliente;
```

Resultado:

| Inicio |
| -------- |
| Ana    |
| Lui    |
| Mar    |

Y desde el final.

```sql
SELECT
    RIGHT(Nombre,4) AS Final
FROM Cliente;
```

Estas funciones son útiles para trabajar con códigos, matrículas o identificadores.

---

## SUBSTRING()

Permite extraer una parte concreta del texto.

```sql
SELECT
    SUBSTRING(Nombre,2,4) AS Fragmento
FROM Cliente;
```

Parámetros:

* posición inicial;
* número de caracteres.

Resulta especialmente útil cuando los datos siguen un formato fijo.

---

## TRIM()

Elimina espacios innecesarios al principio y al final del texto.

```sql
SELECT
    TRIM(Nombre)
FROM Cliente;
```

Es muy utilizada tras importar datos desde hojas de cálculo o archivos CSV.

---

## REPLACE()

Permite sustituir una cadena por otra.

```sql
SELECT
    REPLACE(Correo,
            '@empresa.com',
            '@universidad.edu')
AS NuevoCorreo
FROM Empleado;
```

Ideal para realizar transformaciones masivas sobre información textual.

---

## Buenas prácticas

Las funciones de cadena deben utilizarse para mejorar la presentación o transformar datos, pero conviene evitar abusar de ellas sobre tablas muy grandes, ya que incrementan el trabajo del servidor.

Siempre que sea posible, es recomendable almacenar la información correctamente desde el principio.

---

## Ideas clave

* Las funciones de cadena trabajan sobre cada fila individualmente.
* `UPPER()` y `LOWER()` cambian el uso de mayúsculas y minúsculas.
* `CONCAT()` une varias cadenas.
* `LENGTH()` devuelve el número de caracteres.
* `LEFT()`, `RIGHT()` y `SUBSTRING()` extraen partes de un texto.
* `TRIM()` elimina espacios innecesarios.
* `REPLACE()` sustituye fragmentos de texto.

