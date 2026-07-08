# SQL no nació primero

## Introducción

Cuando los estudiantes comienzan a trabajar con bases de datos suele parecer que SQL ha existido desde siempre y que constituye el fundamento de todas las bases de datos relacionales. Sin embargo, la historia fue exactamente la contraria.

SQL no creó el modelo relacional. SQL fue creado para poder utilizar un modelo relacional que ya existía y cuya base matemática estaba perfectamente definida.

Comprender este orden histórico resulta importante porque explica muchas características del propio lenguaje SQL. Algunas de sus decisiones de diseño, su sintaxis e incluso algunas aparentes inconsistencias solo pueden entenderse conociendo el camino que siguió su evolución.

En este capítulo recorreremos brevemente esa historia para comprender por qué primero apareció el Álgebra Relacional y posteriormente surgieron lenguajes como SQL.

### Antes de SQL

Durante las décadas de 1960 y principios de 1970 las bases de datos más utilizadas eran jerárquicas o en red.

En estos sistemas el programador debía conocer la estructura física de almacenamiento y navegar manualmente entre registros mediante punteros.

Por ejemplo, para localizar todos los pedidos de un cliente era necesario recorrer explícitamente la estructura de almacenamiento. El programador indicaba paso a paso qué camino debía seguir el sistema para encontrar la información.

Este enfoque presentaba varios inconvenientes:

* Los programas dependían completamente de la organización física de los datos.
* Un pequeño cambio en la estructura obligaba a modificar numerosas aplicaciones.
* Las consultas complejas resultaban difíciles de escribir y mantener.
* No existía independencia entre los datos y los programas.

La programación de bases de datos se parecía más a recorrer una estructura de memoria que a formular preguntas sobre la información almacenada.

### El cambio de paradigma

En 1970, Edgar F. Codd propuso una idea revolucionaria: el usuario no debía indicar **cómo** buscar los datos, sino **qué** información necesitaba obtener.

Esta diferencia puede parecer sutil, pero transformó completamente el diseño de las bases de datos.

En lugar de navegar entre registros, las consultas podían describirse como una sucesión de operaciones matemáticas aplicadas sobre conjuntos de datos.

El Álgebra Relacional proporcionó precisamente ese conjunto de operaciones.

### Del Álgebra Relacional a SEQUEL

Una vez establecido el modelo teórico, surgió una nueva necesidad: disponer de un lenguaje práctico que pudiera ser utilizado por analistas, desarrolladores y administradores de bases de datos.

A mediados de la década de 1970, investigadores de IBM desarrollaron un lenguaje experimental denominado **SEQUEL** (Structured English Query Language).

Su objetivo era ofrecer una sintaxis cercana al inglés que permitiera expresar muchas de las operaciones descritas por el Álgebra Relacional sin necesidad de utilizar símbolos matemáticos.

Posteriormente, por motivos legales relacionados con la marca registrada "SEQUEL", el lenguaje pasó a denominarse simplemente ​**SQL (Structured Query Language)**​.

### ¿Es SQL el Álgebra Relacional?

No exactamente.

SQL está profundamente inspirado en el Álgebra Relacional, pero no es una implementación literal de esta.

Existen varias diferencias importantes.

Por ejemplo:

| Álgebra Relacional                        | SQL                                                |
| -------------------------------------------- | ---------------------------------------------------- |
| Basada en teoría de conjuntos             | Basado en bolsas o multiconjuntos por defecto      |
| No admite filas duplicadas                 | Puede devolver duplicados                          |
| Es completamente declarativa y matemática | Incorpora aspectos prácticos y de implementación |
| Define operadores formales                 | Define una sintaxis orientada a los usuarios       |

A pesar de estas diferencias, prácticamente todas las consultas SQL pueden interpretarse como una combinación de operadores del Álgebra Relacional.

### ¿Por qué seguimos estudiando Álgebra Relacional?

Puede surgir una pregunta razonable:

> Si en la práctica utilizaremos SQL, ¿por qué dedicar tiempo al Álgebra Relacional?

La respuesta es sencilla.

Porque el Álgebra Relacional permite comprender cómo transforma internamente un SGBD una consulta SQL.

Cuando escribimos una consulta aparentemente sencilla como:

```sql
SELECT Nombre
FROM Cliente
WHERE Ciudad = 'Santander';
```

el motor de la base de datos no ejecuta directamente ese texto.

Primero lo analiza, lo transforma en una representación basada en operadores algebraicos, optimiza dicha representación y finalmente genera un plan de ejecución eficiente.

En otras palabras, aunque el desarrollador escriba SQL, el motor continúa "pensando" en términos de Álgebra Relacional.

### Relación con nuestro caso de estudio

Durante el resto del curso seguiremos utilizando la base de datos de nuestra empresa de venta de productos tecnológicos.

Cada consulta SQL que escribamos podrá interpretarse previamente como una secuencia de operaciones algebraicas.

Esta forma de razonar nos permitirá comprender mejor el comportamiento de las consultas, detectar errores con mayor facilidad y escribir código más eficiente.

### Errores frecuentes

Uno de los errores más habituales consiste en pensar que SQL define el modelo relacional.

En realidad ocurre lo contrario: el modelo relacional y el Álgebra Relacional existían antes que SQL y sirvieron como fundamento para su diseño.

Otro error frecuente es creer que el motor ejecuta literalmente la consulta escrita por el usuario. En realidad, el sistema la transforma y optimiza antes de acceder a los datos.

### Ideas clave

* El Álgebra Relacional apareció antes que SQL.
* SQL nació como una forma práctica de expresar operaciones algebraicas.
* El modelo relacional es independiente de SQL.
* Los motores de bases de datos transforman las consultas SQL en operaciones algebraicas internas.
* Comprender esta relación facilitará el aprendizaje de SQL y permitirá interpretar mejor el funcionamiento de los SGBD.

