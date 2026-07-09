# Traducción de Álgebra Relacional a SQL

## Introducción

Hasta este momento del curso hemos estudiado los operadores fundamentales del Álgebra Relacional y hemos establecido la correspondencia individual entre cada uno de ellos y las principales cláusulas de SQL. Sin embargo, un profesional rara vez se enfrenta a expresiones aisladas. En la práctica, las consultas suelen combinar varias operaciones y el reto consiste en transformarlas correctamente en una sentencia SQL equivalente.

Traducir una expresión de Álgebra Relacional a SQL no consiste en sustituir símbolos por palabras reservadas. Es un proceso de análisis en el que debemos identificar qué hace cada operador, en qué orden actúa y cómo se expresa esa lógica utilizando la sintaxis de SQL.

Una buena traducción debe preservar exactamente el significado de la expresión original. Dos consultas pueden escribirse de forma diferente, pero solo serán equivalentes si producen el mismo conjunto de resultados.

En este capítulo aprenderemos una metodología que permitirá traducir expresiones sencillas y complejas de manera sistemática.

### ¿Por dónde empezar?

Uno de los errores más frecuentes consiste en observar una expresión algebraica completa e intentar escribir inmediatamente la consulta SQL.

Cuando las expresiones son pequeñas este método puede funcionar, pero deja de ser útil en cuanto aparecen varios operadores anidados.

Resulta mucho más sencillo dividir el problema en una serie de preguntas.

1. ¿Qué relaciones intervienen?
2. ¿Qué relaciones deben combinarse?
3. ¿Qué condiciones deben cumplirse?
4. ¿Qué atributos deben mostrarse?
5. ¿Existen operaciones de conjuntos?

Responder a estas preguntas permite construir la consulta SQL de forma ordenada y reduce considerablemente la probabilidad de cometer errores.

### Método general de traducción

Podemos resumir el proceso mediante la siguiente tabla.

| Álgebra Relacional        | SQL         |
| ---------------------------- | ------------- |
| Relaciones utilizadas      | FROM        |
| Producto cartesiano o JOIN | FROM + JOIN |
| Selección (σ)            | WHERE       |
| Proyección (π)           | SELECT      |
| Unión                     | UNION       |
| Intersección              | INTERSECT   |
| Diferencia                 | EXCEPT      |

Obsérvese que el orden de escritura cambia.

En Álgebra Relacional la proyección suele aparecer como la operación más externa.

En SQL, por el contrario, la cláusula SELECT se escribe al comienzo de la consulta.

Esta diferencia sintáctica no modifica el significado de la operación.

### Ejemplo 1. Selección y proyección

Consideremos la siguiente expresión:

```text
π Nombre
(
    σ Ciudad='Santander'
    (
        Cliente
    )
)
```

Analicemos la consulta paso a paso.

La relación utilizada es:

* Cliente.

La condición es:

* Ciudad = 'Santander'.

El atributo solicitado es:

* Nombre.

La traducción directa es:

```sql
SELECT Nombre
FROM Cliente
WHERE Ciudad = 'Santander';
```

Puede comprobarse que el operador más externo del Álgebra Relacional, la proyección, termina convirtiéndose en la cláusula SELECT.

La selección pasa a convertirse en la cláusula WHERE.

### Ejemplo 2. Dos relaciones

Ahora consideremos una consulta ligeramente más compleja.

```text
π Nombre, Fecha
(
    Cliente
    ⋈ Cliente.IdCliente = Pedido.IdCliente
    Pedido
)
```

Antes de escribir SQL debemos identificar los elementos de la expresión.

Relaciones:

* Cliente
* Pedido

Condición de unión:

* Cliente.IdCliente = Pedido.IdCliente

Atributos solicitados:

* Nombre
* Fecha

La traducción es:

```sql
SELECT c.Nombre,
       p.Fecha
FROM Cliente c
INNER JOIN Pedido p
    ON c.IdCliente = p.IdCliente;
```

Obsérvese que la condición de unión ya no aparece como una selección independiente.

SQL incorpora una sintaxis específica mediante **INNER JOIN** y **ON** que expresa exactamente la misma relación lógica.

### Ejemplo 3. Tres relaciones

Supongamos ahora que deseamos obtener el nombre del cliente y el nombre del producto adquirido.

En Álgebra Relacional:

```text
π Cliente.Nombre, Producto.Nombre
(
    Cliente
    ⋈ Pedido
    ⋈ LineaPedido
    ⋈ Producto
)
```

Aunque la expresión se ha simplificado para destacar el recorrido, conceptualmente representa la unión de cuatro relaciones.

La traducción a SQL sería:

```sql
SELECT c.Nombre,
       pr.Nombre
FROM Cliente c
INNER JOIN Pedido p
    ON c.IdCliente = p.IdCliente
INNER JOIN LineaPedido lp
    ON p.IdPedido = lp.IdPedido
INNER JOIN Producto pr
    ON lp.IdProducto = pr.IdProducto;
```

Puede observarse que el recorrido entre las tablas es exactamente el mismo en ambos lenguajes.

### Una estrategia muy recomendable

Cuando las consultas son largas resulta útil realizar primero un pequeño esquema.

Por ejemplo:

```
Relaciones:
Cliente
Pedido
LineaPedido
Producto

Filtros:
Ciudad = Santander
Precio > 300

Resultado:
NombreCliente
NombreProducto
Precio
```

Una vez identificado el recorrido resulta mucho más sencillo escribir la consulta SQL.

Esta técnica es ampliamente utilizada por desarrolladores y administradores de bases de datos, ya que reduce el número de errores y facilita la revisión del código.

### Casos reales

En un sistema de comercio electrónico es habitual traducir consultas diseñadas inicialmente sobre el modelo relacional a sentencias SQL que posteriormente se incorporarán a aplicaciones web, sistemas ERP o herramientas de inteligencia de negocio.

Comprender la equivalencia entre ambos lenguajes permite verificar que la consulta implementada en SQL refleja correctamente el problema planteado durante la fase de análisis.

### Errores frecuentes

Un error habitual consiste en comenzar escribiendo la cláusula SELECT sin haber identificado previamente todas las relaciones necesarias.

Otro error muy común es olvidar alguna de las condiciones de unión cuando intervienen varias tablas, lo que produce productos cartesianos no deseados y resultados incorrectos.

También es frecuente traducir literalmente la estructura del Álgebra Relacional, olvidando que SQL posee una organización sintáctica diferente.

### Ideas clave

* Traducir Álgebra Relacional a SQL consiste en conservar el significado de la consulta, no su forma.
* Antes de escribir SQL conviene identificar relaciones, condiciones y atributos.
* Cada operador relacional posee una cláusula SQL equivalente.
* El orden sintáctico cambia entre ambos lenguajes, pero la lógica permanece inalterada.
* Utilizar un esquema previo facilita la construcción de consultas complejas y reduce la aparición de errores.
  

