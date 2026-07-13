# COUNT

## Introducción

La función `COUNT()` es, probablemente, la función de agregación más utilizada en SQL.

Su objetivo es muy sencillo:

> **Contar registros.**

Aunque la idea parece simple, `COUNT()` posee varias formas de uso y es importante comprender las diferencias entre ellas para evitar resultados incorrectos.

---

## COUNT(\*)

La forma más habitual consiste en utilizar un asterisco.

```sql
SELECT
    COUNT(*)
FROM Cliente;
```

Resultado:

| COUNT(\*) |
| ----------: |
|       250 |

La consulta indica que existen 250 clientes registrados.

`COUNT(*)` cuenta **todas las filas** de la tabla.

No importa si alguna columna contiene valores `NULL`.

---

## COUNT(columna)

También podemos indicar una columna concreta.

```sql
SELECT
    COUNT(Telefono)
FROM Cliente;
```

En este caso únicamente se cuentan las filas cuyo teléfono ​**no sea NULL**​.

Supongamos la siguiente información.

| Cliente | Teléfono |
| --------- | ----------- |
| Ana     | 612345678 |
| Luis    | NULL      |
| Marta   | 654987321 |
| Pedro   | NULL      |

La consulta devolvería:

| COUNT(Telefono) |
| ----------------: |
|               2 |

Solo dos registros contienen un teléfono válido.

---

## COUNT(DISTINCT)

También es posible contar valores diferentes.

```sql
SELECT
    COUNT(DISTINCT Ciudad)
FROM Cliente;
```

Resultado:

| COUNT(DISTINCT Ciudad) |
| -----------------------: |
|                     12 |

Aunque existan cientos de clientes, únicamente se cuentan las ciudades distintas.

Esta técnica resulta muy útil para obtener estadísticas rápidas.

---

## COUNT con WHERE

`COUNT()` puede combinarse con filtros.

```sql
SELECT
    COUNT(*)
FROM Producto
WHERE Activo = TRUE;
```

La consulta cuenta únicamente los productos activos.

El proceso sigue el orden lógico de ejecución:

1. Se selecciona la tabla.
2. Se aplica `WHERE`.
3. Se ejecuta `COUNT()`.

---

## COUNT con alias

Es recomendable asignar un nombre descriptivo.

```sql
SELECT
    COUNT(*) AS TotalClientes
FROM Cliente;
```

Resultado:

| TotalClientes |
| --------------: |
|           250 |

Esto facilita la lectura del resultado y simplifica el trabajo con aplicaciones que consumen la consulta.

---

## Aplicaciones reales

`COUNT()` aparece constantemente en sistemas de información.

Algunos ejemplos:

* número de clientes registrados;
* productos en stock;
* empleados por departamento;
* pedidos pendientes;
* incidencias abiertas;
* facturas emitidas durante un período.

Es una de las funciones más utilizadas en informes empresariales.

---

## Errores frecuentes

Los errores más habituales son:

* confundir `COUNT(*)` con `COUNT(columna)`;
* olvidar que `COUNT(columna)` ignora los valores `NULL`;
* no utilizar alias para el resultado;
* pensar que `COUNT()` devuelve las filas en lugar del número de filas.

---

## Ideas clave

* `COUNT()` cuenta registros.
* `COUNT(*)` cuenta todas las filas.
* `COUNT(columna)` ignora los valores `NULL`.
* `COUNT(DISTINCT columna)` cuenta únicamente valores diferentes.
* Es una de las funciones más utilizadas en SQL y constituye la base de numerosos informes y estadísticas.

