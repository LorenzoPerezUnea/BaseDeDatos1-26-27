# Prompt para generar un dataset de prácticas SQL

Quiero practicar SQL utilizando una base de datos sobre ​**[TEMA ELEGIDO POR EL ALUMNO]**​.

Genera un conjunto de datos completo y coherente para poder practicar consultas SQL progresivamente, desde consultas sencillas sobre una tabla hasta consultas que relacionen varias tablas.

## Estructura de la base de datos

Crea una base de datos formada por ​**5 o 6 tablas relacionadas entre sí**​.

Debe existir un modelo relacional coherente, con:

* claves primarias;
* claves foráneas;
* relaciones 1:N y, si resulta natural para el tema, alguna relación N:M mediante una tabla intermedia;
* nombres de tablas y columnas claros;
* tipos de datos apropiados.

El modelo debe representar un pequeño sistema realista relacionado con el tema elegido.

## Cantidad de datos

Genera ​**suficientes registros para poder realizar consultas interesantes**​.

Como referencia:

* tablas principales: al menos 20–30 registros;
* tablas intermedias o de detalle: al menos 50–100 registros;
* si alguna tabla necesita más registros para que las consultas de agregación sean significativas, genera los que sean necesarios.

Los datos deben ser variados y coherentes.

Debe haber:

* valores numéricos diferentes;
* fechas distribuidas en distintos meses y años;
* diferentes categorías, tipos o estados;
* nombres y textos variados;
* relaciones entre registros;
* algunos valores `NULL` cuando tengan sentido;
* registros que tengan relaciones y otros que no las tengan, cuando el modelo lo permita.

Esto permitirá practicar posteriormente `INNER JOIN` y `LEFT JOIN`.

## Calidad de los datos

Los datos deben respetar las restricciones de integridad referencial.

No debe haber claves foráneas que apunten a registros inexistentes.

Debe existir suficiente variedad para que posteriormente puedan plantearse consultas que:

* filtren resultados;
* ordenen datos;
* calculen valores;
* agrupen registros;
* calculen sumas, medias, mínimos y máximos;
* trabajen con fechas;
* trabajen con cadenas de caracteres;
* relacionen varias tablas;
* detecten registros sin correspondencia mediante `LEFT JOIN`;
* utilicen `EXISTS`, `ANY` u operadores similares.

No introduzcas datos artificialmente repetitivos. Los valores deben parecer pertenecientes a un sistema real.

## Formato de salida

Entrega:

1. Una breve descripción del sistema.
2. La estructura de las 5 o 6 tablas.
3. Las relaciones entre las tablas.
4. Las sentencias `CREATE TABLE`.
5. Las sentencias `INSERT INTO` necesarias para cargar todos los datos.
6. Una breve descripción de qué tipo de información contiene cada tabla.

Utiliza SQL estándar siempre que sea posible.

No generes ejercicios ni soluciones SQL todavía. En este paso únicamente necesito **crear y poblar la base de datos** que utilizaré posteriormente para practicar.

# Prompt 1 — SELECT sobre una sola tabla

Utiliza exclusivamente la base de datos sobre **[TEMA]** que se ha generado anteriormente.

Quiero una colección de **ejercicios propuestos de SQL** centrados inicialmente en consultas sobre ​**una única tabla**​.

Los ejercicios deben practicar progresivamente:

* `SELECT`;
* selección de columnas concretas;
* `WHERE`;
* operadores de comparación;
* `AND`, `OR` y `NOT`;
* `IN`, `BETWEEN` y `LIKE`;
* `IS NULL` e `IS NOT NULL`;
* `ORDER BY`;
* alias de columnas;
* expresiones aritméticas;
* funciones aritméticas sencillas;
* funciones de cadenas de caracteres;
* funciones relacionadas con fechas.

Todos los ejercicios de esta serie deben poder resolverse ​**sin JOIN**​.

También deben evitarse:

* subconsultas;
* `GROUP BY`;
* funciones de agregación como `SUM`, `AVG`, `COUNT`, `MIN` o `MAX`.

Quiero que los ejercicios sean acumulativos: los últimos deben combinar varias de las técnicas aprendidas anteriormente.

## Formato de cada ejercicio

Para cada ejercicio proporciona:

### Ejercicio N: [título]

**Enunciado:**
Describe claramente qué información debe obtener el alumno.

**Pista:**
Proporciona una pequeña orientación sobre qué cláusula, operador o función podría necesitar, pero ​**sin mostrar la consulta ni la solución**​.

No proporciones:

* código SQL de respuesta;
* pseudocódigo que revele la solución;
* explicación paso a paso de la solución.

Genera entre ​**10 y 15 ejercicios**​, comenzando con consultas muy sencillas y terminando con consultas que combinen varios filtros, ordenaciones, funciones de cadenas, funciones de fechas y expresiones aritméticas.

El nivel debe ser apropiado para un alumno que está comenzando a dominar DQL.

---

# Prompt 2 — Agregación y agrupación sobre una sola tabla

Utiliza exclusivamente la base de datos sobre **[TEMA]** que se ha generado anteriormente.

Quiero una colección de **ejercicios propuestos de SQL** que continúe progresivamente desde los ejercicios anteriores.

Todos los ejercicios deben seguir trabajando inicialmente con ​**una única tabla**​, pero ahora deben introducir y combinar:

* funciones de agregación:
  * `COUNT`;
  * `SUM`;
  * `AVG`;
  * `MIN`;
  * `MAX`;
* `GROUP BY`;
* `HAVING`;
* `ORDER BY`;
* funciones de fechas;
* funciones de cadenas de caracteres;
* expresiones y funciones aritméticas;
* filtros mediante `WHERE`.

Los ejercicios deben ser acumulativos. Los primeros deben introducir las funciones de agregación de forma sencilla y los últimos deben combinar varias técnicas en una misma consulta.

## Restricciones

No utilices:

* `JOIN`;
* `LEFT JOIN`;
* `RIGHT JOIN`;
* `FULL JOIN`;
* `EXISTS`;
* `ANY`;
* `ALL`;
* subconsultas de ningún tipo.

La intención es que el alumno aprenda primero a resolver consultas de agregación y agrupación ​**sobre una sola tabla**​.

## Formato de cada ejercicio

Para cada ejercicio proporciona:

### Ejercicio N: [título]

**Enunciado:**
Describe claramente qué debe obtener el alumno.

**Pista:**
Da una orientación breve sobre qué función de agregación, agrupación, filtro, función de fecha, función de cadena o expresión aritmética puede ser necesaria.

La pista ​**no debe contener la consulta ni revelar directamente la solución**​.

No proporciones código SQL de respuesta.

Genera entre ​**10 y 15 ejercicios**​, ordenados de menor a mayor dificultad.

Los últimos ejercicios deben combinar, por ejemplo, `WHERE`, `GROUP BY`, `HAVING`, funciones de agregación y `ORDER BY` en una misma consulta.

---

# Prompt 3 — JOIN y consultas con varias tablas

Utiliza exclusivamente la base de datos sobre **[TEMA]** que se ha generado anteriormente.

Quiero una nueva colección de **ejercicios propuestos de SQL** que continúe de forma acumulativa los dos bloques anteriores.

A partir de este bloque quiero introducir consultas que trabajen con ​**dos o más tablas relacionadas**​.

Los ejercicios deben introducir progresivamente:

* `INNER JOIN`;
* varios `INNER JOIN` consecutivos;
* `LEFT JOIN`;
* combinaciones de `INNER JOIN` y `LEFT JOIN`;
* condiciones de unión mediante `ON`;
* filtros mediante `WHERE`;
* `ORDER BY`;
* funciones de agregación;
* `GROUP BY`;
* `HAVING`;
* funciones de cadenas;
* funciones de fechas;
* expresiones aritméticas;
* `EXISTS`;
* `ANY` cuando tenga sentido en el modelo;
* combinaciones de varias de estas técnicas.

La dificultad debe aumentar progresivamente.

## Orden de dificultad

Comienza con:

1. un `INNER JOIN` entre dos tablas;
2. un `JOIN` entre tres tablas;
3. varios `JOIN` consecutivos;
4. `JOIN` combinado con filtros;
5. `JOIN` combinado con `ORDER BY`;
6. `JOIN` combinado con expresiones aritméticas;
7. `JOIN` combinado con `GROUP BY` y agregaciones;
8. varios `JOIN` con `GROUP BY`, `HAVING` y `ORDER BY`;
9. `LEFT JOIN` para encontrar registros que no tienen correspondencia;
10. varios `LEFT JOIN`;
11. combinación de `INNER JOIN` y `LEFT JOIN`;
12. consultas que utilicen `EXISTS`;
13. consultas que utilicen `ANY` cuando el modelo lo permita;
14. ejercicios finales que combinen varias de las técnicas anteriores.

## Restricción importante

**No utilices subconsultas.**

No deben aparecer:

* subconsultas en `SELECT`;
* subconsultas en `FROM`;
* subconsultas en `WHERE`;
* subconsultas en `HAVING`.

Tampoco utilices `WITH` ni CTE.

La finalidad es practicar exclusivamente la construcción de consultas mediante las herramientas estudiadas hasta este momento: filtros, funciones, agregaciones, agrupaciones, ordenación, `JOIN`, `LEFT JOIN`, `EXISTS` y `ANY`.

Las consultas anidadas se estudiarán en una clase posterior y, por tanto, ​**no deben aparecer en estos ejercicios**​.

## Formato de cada ejercicio

Para cada ejercicio proporciona:

### Ejercicio N: [título]

**Enunciado:**
Describe de forma clara qué información debe obtener el alumno y qué condiciones debe cumplir el resultado.

**Pista:**
Incluye únicamente una orientación breve que ayude al alumno a decidir qué técnica necesita.

La pista puede mencionar, por ejemplo:

* qué tablas tendrá que relacionar;
* que necesitará un `LEFT JOIN`;
* que deberá agrupar;
* que tendrá que utilizar una función de agregación;
* que puede necesitar `EXISTS` o `ANY`.

Pero ​**no escribas la consulta ni reveles la solución**​.

No proporciones:

* código SQL de respuesta;
* pseudocódigo;
* solución paso a paso;
* explicación detallada de cómo construir la consulta.

Genera entre ​**15 y 20 ejercicios**​, ordenados estrictamente de menor a mayor dificultad.

Los últimos ejercicios deben combinar varias tablas y varias de las técnicas anteriores, pero sin utilizar consultas anidadas.

