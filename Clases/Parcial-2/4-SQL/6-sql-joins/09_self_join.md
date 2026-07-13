# SELF JOIN

## Introducción

Hasta ahora todos los `JOIN` relacionaban ​**dos tablas distintas**​.

Sin embargo, existen situaciones en las que una tabla necesita relacionarse consigo misma.

Para ello utilizamos el ​**SELF JOIN**​.

Aunque su nombre pueda parecer complejo, en realidad no es un nuevo tipo de JOIN.

Simplemente consiste en realizar un `JOIN` entre ​**dos copias lógicas de la misma tabla**​, utilizando alias diferentes.

---

## ¿Cuándo se utiliza?

El caso más habitual aparece cuando una tabla contiene relaciones jerárquicas.

Por ejemplo:

### Empleado

| IdEmpleado | Nombre   | IdSupervisor |
| -----------: | ---------- | -------------: |
|          1 | Director |         NULL |
|          2 | Ana      |            1 |
|          3 | Luis     |            1 |
|          4 | Marta    |            2 |

La columna `IdSupervisor` hace referencia a otro empleado de la misma tabla.

---

## El problema

Queremos obtener un resultado como:

| Empleado | Supervisor |
| ---------- | ------------ |
| Ana      | Director   |
| Luis     | Director   |
| Marta    | Ana        |

Toda la información se encuentra en una única tabla.

Necesitamos leerla dos veces.

---

## Solución mediante SELF JOIN

```sql
SELECT
    e.Nombre AS Empleado,
    s.Nombre AS Supervisor
FROM Empleado AS e
LEFT JOIN Empleado AS s
ON e.IdSupervisor = s.IdEmpleado;
```

Observa que la tabla `Empleado` aparece dos veces.

No son dos tablas distintas.

Son dos **alias** que representan dos roles diferentes:

* `e` representa al empleado.
* `s` representa al supervisor.

---

## ¿Por qué son necesarios los alias?

Sin alias, MySQL no sabría a qué copia de la tabla pertenece cada columna.

Los alias permiten distinguir claramente ambos papeles.

```text
Empleado

        │

 ┌──────┴──────┐

Empleado     Empleado

   e            s

Empleado    Supervisor
```

Esta es la esencia de un `SELF JOIN`.

---

## Otros ejemplos

Los SELF JOIN aparecen con frecuencia en modelos jerárquicos.

Por ejemplo:

* empleados y supervisores;
* categorías y subcategorías;
* comentarios y respuestas;
* carpetas y subcarpetas;
* personas y padres.

Siempre que una fila haga referencia a otra fila de la misma tabla, un `SELF JOIN` suele ser una buena solución.

---

## SELF JOIN con INNER JOIN

Si sabemos que todos los empleados tienen supervisor, podríamos utilizar:

```sql
SELECT
    e.Nombre,
    s.Nombre
FROM Empleado AS e
INNER JOIN Empleado AS s
ON e.IdSupervisor = s.IdEmpleado;
```

Sin embargo, normalmente el director general no tiene supervisor.

Por ello suele utilizarse `LEFT JOIN` para conservar también ese registro.

---

## Buenas prácticas

Cuando utilices un `SELF JOIN`:

* emplea alias descriptivos (`Empleado`, `Supervisor`, `Padre`, `Hijo`, etc.);
* documenta claramente el papel de cada alias;
* revisa cuidadosamente la condición del `ON`;
* evita nombres ambiguos en el `SELECT`.

Esto facilita enormemente la comprensión de la consulta.

---

## Ideas clave

* Un `SELF JOIN` relaciona una tabla consigo misma.
* No es un nuevo tipo de JOIN, sino una aplicación de los JOIN ya conocidos.
* Los alias son imprescindibles para diferenciar cada copia lógica de la tabla.
* Es muy utilizado para representar jerarquías y relaciones recursivas.
* Constituye una herramienta fundamental en modelos organizativos y estructuras en árbol.

