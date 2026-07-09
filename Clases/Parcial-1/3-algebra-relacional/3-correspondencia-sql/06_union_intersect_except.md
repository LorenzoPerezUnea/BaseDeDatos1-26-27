# UNION, INTERSECT y EXCEPT

## Introducción

En las clases anteriores se estudiaron las **operaciones de conjuntos** del Álgebra Relacional. A diferencia de la selección o la proyección, que actúan sobre una única relación, estas operaciones permiten combinar los resultados de dos consultas distintas para construir una nueva relación.

Desde un punto de vista matemático, estas operaciones proceden directamente de la teoría de conjuntos. Por este motivo, conservan prácticamente el mismo significado tanto en Álgebra Relacional como en SQL.

Sin embargo, existe una diferencia importante: mientras que en el Álgebra Relacional las relaciones son conjuntos y, por tanto, ​**no contienen duplicados**​, SQL trabaja por defecto con **multiconjuntos** (​*bags*​). Esta característica influye en el comportamiento de estas operaciones y constituye una de las principales diferencias entre ambos lenguajes.

En este capítulo estudiaremos cómo se traducen la ​**unión**​, la **intersección** y la **diferencia** desde el Álgebra Relacional hasta SQL, utilizando siempre el mismo caso de estudio de la empresa comercial.

### Las operaciones de conjuntos en el Álgebra Relacional

Recordemos las tres operaciones fundamentales:

| Operador | Nombre        | Significado                                                     |
| ---------- | --------------- | ----------------------------------------------------------------- |
| ∪       | Unión        | Tuplas que aparecen en cualquiera de las dos relaciones.        |
| ∩       | Intersección | Tuplas comunes a ambas relaciones.                              |
| −       | Diferencia    | Tuplas presentes en la primera relación pero no en la segunda. |

Todas ellas requieren que las relaciones sean ​**compatibles por unión**​, es decir, que tengan el mismo número de atributos y que cada posición corresponda a dominios compatibles.

Por ejemplo, si disponemos de dos relaciones que contienen ciudades donde existen almacenes y ciudades donde existen tiendas físicas:

**CiudadesAlmacenes**

| Ciudad    |
| ----------- |
| Santander |
| Bilbao    |
| Oviedo    |

**CiudadesTiendas**

| Ciudad    |
| ----------- |
| Bilbao    |
| Madrid    |
| Santander |

Estas relaciones pueden combinarse mediante operaciones de conjuntos.

---

### UNION

En Álgebra Relacional:

```text
CiudadesAlmacenes ∪ CiudadesTiendas
```

Resultado:

| Ciudad    |
| ----------- |
| Santander |
| Bilbao    |
| Oviedo    |
| Madrid    |

La traducción a SQL es directa:

```sql
SELECT Ciudad
FROM CiudadesAlmacenes

UNION

SELECT Ciudad
FROM CiudadesTiendas;
```

Puede observarse que ​**UNION elimina automáticamente los duplicados**​, reproduciendo el comportamiento del Álgebra Relacional.

#### UNION ALL

SQL incorpora además una variante que no existe en el Álgebra Relacional clásica.

```sql
SELECT Ciudad
FROM CiudadesAlmacenes

UNION ALL

SELECT Ciudad
FROM CiudadesTiendas;
```

En este caso se conservan todas las filas, incluso aquellas que aparecen repetidas.

Esta operación suele ser más rápida porque evita el proceso de eliminación de duplicados.

En aplicaciones reales se utiliza cuando las repeticiones tienen significado o cuando se desea maximizar el rendimiento.

---

### INTERSECT

La intersección conserva únicamente los elementos comunes.

Álgebra Relacional:

```text
CiudadesAlmacenes ∩ CiudadesTiendas
```

Resultado:

| Ciudad    |
| ----------- |
| Bilbao    |
| Santander |

En SQL:

```sql
SELECT Ciudad
FROM CiudadesAlmacenes

INTERSECT

SELECT Ciudad
FROM CiudadesTiendas;
```

Conceptualmente ambas expresiones son idénticas.

No obstante, conviene señalar que ​**INTERSECT no está disponible en todos los SGBD**​. Algunos motores antiguos o determinadas versiones de MySQL no implementan este operador de forma nativa, obligando a utilizar otras estrategias que se estudiarán más adelante en el curso.

---

### EXCEPT

La diferencia permite localizar los elementos que pertenecen a la primera relación pero no aparecen en la segunda.

Álgebra Relacional:

```text
CiudadesAlmacenes − CiudadesTiendas
```

Resultado:

| Ciudad |
| -------- |
| Oviedo |

En SQL:

```sql
SELECT Ciudad
FROM CiudadesAlmacenes

EXCEPT

SELECT Ciudad
FROM CiudadesTiendas;
```

Esta consulta devuelve únicamente las ciudades donde existen almacenes pero no tiendas físicas.

Al igual que ocurre con INTERSECT, algunos sistemas gestores utilizan la palabra reservada **MINUS** en lugar de ​**EXCEPT**​, mientras que otros no implementan ninguna de las dos y requieren técnicas alternativas.

---

### Compatibilidad por unión en SQL

Las mismas restricciones estudiadas en el Álgebra Relacional siguen siendo válidas.

Por ejemplo, esta consulta es correcta:

```sql
SELECT Nombre, Ciudad
FROM Cliente

UNION

SELECT Nombre, Ciudad
FROM Proveedor;
```

Ambas consultas generan exactamente dos columnas compatibles.

En cambio, esta consulta produciría un error:

```sql
SELECT Nombre
FROM Cliente

UNION

SELECT Nombre, Ciudad
FROM Proveedor;
```

La primera consulta devuelve una columna y la segunda devuelve dos.

El motor SQL rechazará la operación porque ambas consultas no producen relaciones compatibles.

---

### Casos reales

Las operaciones de conjuntos aparecen con frecuencia en sistemas empresariales.

Algunos ejemplos son:

* obtener todos los clientes que compran tanto en tiendas físicas como en la tienda en línea;
* localizar productos presentes en dos almacenes diferentes;
* encontrar clientes registrados que todavía no han realizado pedidos;
* combinar listas de proveedores nacionales e internacionales;
* identificar campañas comerciales dirigidas a grupos parcialmente coincidentes de clientes.

En todos estos casos el problema consiste en comparar conjuntos completos de resultados y no registros individuales.

---

### Diferencias importantes respecto al Álgebra Relacional

Aunque la correspondencia es muy directa, conviene recordar varias diferencias.

| Álgebra Relacional                           | SQL                                                                |
| ----------------------------------------------- | -------------------------------------------------------------------- |
| Las relaciones son conjuntos.                 | Los resultados son multiconjuntos por defecto.                     |
| Nunca existen duplicados.                     | Los duplicados se conservan salvo que se eliminen explícitamente. |
| Solo existe la unión clásica.               | Existen UNION y UNION ALL.                                         |
| Todos los operadores forman parte del modelo. | Algunos operadores dependen del SGBD utilizado.                    |

Estas diferencias serán especialmente relevantes cuando el curso se centre en MySQL.

---

### Errores frecuentes

Uno de los errores más habituales consiste en intentar combinar consultas que devuelven distinto número de columnas.

Otro error frecuente es utilizar **UNION** cuando realmente se desea conservar todos los registros. En estos casos debería utilizarse ​**UNION ALL**​, ya que evita el coste adicional de eliminar duplicados.

También es común olvidar que algunos sistemas gestores no implementan **INTERSECT** o ​**EXCEPT**​, lo que obliga a construir consultas equivalentes mediante JOIN, EXISTS o subconsultas.

---

### Ideas clave

* Las operaciones de conjuntos del Álgebra Relacional poseen una correspondencia casi directa en SQL.
* **UNION** combina resultados eliminando duplicados.
* **UNION ALL** conserva todas las filas y suele ofrecer un mejor rendimiento.
* **INTERSECT** devuelve únicamente los registros comunes.
* **EXCEPT** devuelve los registros presentes en la primera consulta y ausentes en la segunda.
* Las consultas participantes deben ser compatibles por unión.
* Aunque los conceptos son los mismos, la disponibilidad de algunos operadores depende del sistema gestor de bases de datos utilizado.

