# Alias

## Introducción

En muchas ocasiones el nombre de una columna almacenada en la base de datos no es el más adecuado para mostrarlo directamente al usuario.

Por ejemplo, una columna llamada:

```text
CorreoElectronico
```

es perfectamente válida desde el punto de vista del diseño de la base de datos, pero quizá resulte demasiado larga para aparecer como encabezado de una tabla o de un informe.

Del mismo modo, una aplicación puede necesitar presentar un título diferente según el contexto.

Para resolver este problema SQL incorpora los ​**alias**​, que permiten asignar nombres temporales tanto a columnas como, más adelante, a tablas.

Los alias ​**no modifican la estructura de la base de datos**​. Únicamente cambian la forma en que se muestran los resultados de una consulta.

---

## ¿Qué es un alias?

Un alias es un nombre alternativo asignado a una columna o a una tabla durante la ejecución de una consulta.

Visualmente:

```text
Base de datos

CorreoElectronico

        │

        ▼

AS Email

        │

        ▼

Resultado

Email
```

El nombre original permanece intacto.

Solo cambia el encabezado mostrado en el resultado.

---

## Sintaxis

La sintaxis más habitual utiliza la palabra clave `AS`.

```sql
SELECT
    Nombre AS Cliente,
    Ciudad AS Localidad
FROM Cliente;
```

Resultado:

| Cliente        | Localidad |
| ---------------- | ----------- |
| Ana Ruiz       | Santander |
| Luis Gómez    | Bilbao    |
| Elena Sánchez | León     |

---

## AS es opcional

En MySQL la palabra `AS` puede omitirse.

Las dos consultas siguientes son equivalentes.

```sql
SELECT
    Nombre AS Cliente
FROM Cliente;
```

```sql
SELECT
    Nombre Cliente
FROM Cliente;
```

Durante esta asignatura utilizaremos preferentemente `AS`, ya que hace el código más legible y facilita su comprensión.

---

## Alias con varias columnas

Podemos asignar un alias a todas las columnas seleccionadas.

```sql
SELECT
    Nombre AS Cliente,
    CorreoElectronico AS Email,
    Ciudad AS CiudadResidencia
FROM Cliente;
```

Resultado:

| Cliente     | Email                                    | CiudadResidencia |
| ------------- | ------------------------------------------ | ------------------ |
| Ana Ruiz    | [ana@empresa.com](mailto:ana@empresa.com)   | Santander        |
| Luis Gómez | [luis@empresa.com](mailto:luis@empresa.com) | Bilbao           |

---

## Alias con espacios

Si el alias contiene espacios debe escribirse entre comillas invertidas (backticks).

```sql
SELECT
    Nombre AS `Nombre del Cliente`,
    CorreoElectronico AS `Correo Electrónico`
FROM Cliente;
```

Resultado:

| Nombre del Cliente | Correo Electrónico                      |
| -------------------- | ------------------------------------------ |
| Ana Ruiz           | [ana@empresa.com](mailto:ana@empresa.com)   |
| Luis Gómez        | [luis@empresa.com](mailto:luis@empresa.com) |

Esta técnica es muy utilizada en informes y paneles de control.

---

## Alias en cálculos

Más adelante aprenderemos a realizar operaciones matemáticas y funciones de agregación.

En esos casos los alias resultan especialmente útiles.

Por ejemplo:

```sql
SELECT
    COUNT(*) AS TotalClientes
FROM Cliente;
```

Aunque todavía no conocemos `COUNT`, este ejemplo permite apreciar cómo los alias mejoran considerablemente la presentación del resultado.

---

## ¿Cuándo utilizar alias?

Los alias son recomendables cuando:

* el nombre de la columna es demasiado largo;
* queremos presentar un encabezado más descriptivo;
* el resultado va a mostrarse directamente al usuario;
* realizamos cálculos cuyo resultado necesita un nombre significativo.

Por el contrario, cuando el nombre original ya resulta claro, no es necesario crear un alias.

---

## Relación con el Álgebra Relacional

En Álgebra Relacional el resultado de una operación podía renombrarse mediante el operador de renombrado (ρ).

En SQL esa misma idea aparece mediante los alias.

Aunque la sintaxis sea diferente, el objetivo es exactamente el mismo: mejorar la legibilidad y facilitar el trabajo con los resultados.

---

## Errores frecuentes

Entre los errores más habituales encontramos:

* pensar que un alias cambia el nombre real de la columna;
* olvidar utilizar comillas invertidas cuando el alias contiene espacios;
* utilizar alias poco descriptivos como `A`, `B` o `X`.

En un entorno profesional conviene utilizar nombres claros y fáciles de interpretar.

---

## Ideas clave

* Un alias asigna un nombre temporal a una columna o tabla.
* La estructura de la base de datos no se modifica.
* La palabra `AS` mejora la legibilidad de las consultas.
* Los alias facilitan la presentación de resultados e informes.
* Más adelante también utilizaremos alias para simplificar consultas sobre varias tablas.

