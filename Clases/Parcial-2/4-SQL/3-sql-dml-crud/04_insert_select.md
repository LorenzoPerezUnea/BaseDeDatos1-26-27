# INSERT ... SELECT

## Introducción

Hasta este momento todas las inserciones realizadas utilizaban valores escritos directamente dentro de la sentencia SQL.

Sin embargo, en muchas ocasiones los datos que queremos insertar ya existen en otra tabla.

Por ejemplo:

* copiar clientes antiguos a una tabla histórica;
* generar una tabla de promociones a partir de los productos existentes;
* crear una lista de clientes VIP utilizando los datos ya almacenados;
* migrar información entre distintas tablas.

En estos casos resulta mucho más eficiente utilizar una consulta `SELECT` como origen de los datos.

Esta técnica recibe el nombre de ​**INSERT ... SELECT**​.

---

## La idea principal

En lugar de escribir manualmente cada valor, dejaremos que otra consulta produzca los registros.

El flujo de trabajo es el siguiente.

```text
Tabla origen

        │

        ▼

SELECT

        │

        ▼

INSERT

        │

        ▼

Tabla destino
```

La consulta obtiene los datos y `INSERT` los almacena automáticamente en otra tabla.

---

## Sintaxis general

La estructura es muy sencilla.

```sql
INSERT INTO TablaDestino
(
    Columna1,
    Columna2
)

SELECT
    ColumnaA,
    ColumnaB
FROM TablaOrigen;
```

Es importante observar que:

* el número de columnas del `SELECT` debe coincidir con el número de columnas del `INSERT`;
* los tipos de datos deben ser compatibles;
* los registros obtenidos por la consulta se insertarán automáticamente.

---

## Primer ejemplo

Supongamos que queremos crear una tabla para almacenar únicamente los nombres de las categorías.

Primero creamos la nueva tabla.

```sql
CREATE TABLE CategoriaResumen
(
    Nombre VARCHAR(80)
);
```

Ahora copiamos la información.

```sql
INSERT INTO CategoriaResumen
(
    Nombre
)

SELECT
    Nombre
FROM Categoria;
```

Todos los nombres de las categorías pasarán automáticamente a la nueva tabla.

---

## Otro ejemplo

Imaginemos una tabla destinada a almacenar únicamente los clientes activos.

```sql
CREATE TABLE ClienteActivo
(
    Nombre VARCHAR(100),
    CorreoElectronico VARCHAR(150)
);
```

La información puede obtenerse directamente mediante una consulta.

```sql
INSERT INTO ClienteActivo
(
    Nombre,
    CorreoElectronico
)

SELECT
    Nombre,
    CorreoElectronico
FROM Cliente
WHERE Activo = TRUE;
```

No hemos escrito manualmente ningún cliente.

La propia consulta selecciona los registros adecuados.

---

## Ventajas

`INSERT ... SELECT` presenta numerosas ventajas.

* Evita introducir datos manualmente.
* Reduce errores de escritura.
* Permite copiar grandes cantidades de información.
* Facilita migraciones entre tablas.
* Aprovecha toda la potencia de las consultas SQL.

En aplicaciones empresariales esta técnica se utiliza constantemente.

---

## Casos reales

Algunos ejemplos habituales son:

* crear tablas históricas;
* generar informes permanentes;
* copiar información entre versiones del sistema;
* consolidar datos procedentes de distintas tablas.

Aunque todavía no conocemos todas las posibilidades de `SELECT`, ya podemos apreciar la enorme utilidad de combinar ambas instrucciones.

---

## Errores frecuentes

El error más habitual consiste en seleccionar un número de columnas diferente al esperado por el `INSERT`.

También es frecuente utilizar columnas cuyos tipos de datos no son compatibles.

Finalmente, algunos estudiantes olvidan que cualquier restricción (`PRIMARY KEY`, `UNIQUE`, `CHECK` o `FOREIGN KEY`) seguirá aplicándose durante la inserción.

### Ideas clave

* `INSERT ... SELECT` copia información obtenida mediante una consulta.
* No es necesario escribir manualmente los valores.
* El número y el tipo de las columnas deben ser compatibles.
* Es una herramienta muy utilizada en migraciones y procesos automáticos.
* Combina la potencia de `INSERT` y `SELECT` en una única operación.

