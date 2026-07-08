# Comparación con SQL

## Introducción

Después de estudiar los fundamentos del Álgebra Relacional es natural preguntarse cuál es su relación con SQL.

A simple vista ambos parecen lenguajes completamente distintos.

El Álgebra Relacional utiliza símbolos matemáticos.

SQL emplea palabras reservadas similares al inglés.

Uno parece diseñado para investigadores.

El otro para desarrolladores.

Sin embargo, esta impresión es engañosa.

En realidad, ambos persiguen exactamente el mismo objetivo: expresar consultas sobre una base de datos relacional.

La principal diferencia radica en la forma en que esas consultas se escriben y en el público al que van dirigidas.

Comprender esta relación permitirá que el aprendizaje de SQL resulte mucho más sencillo durante las próximas clases.

### Dos niveles distintos

Una forma sencilla de entender la diferencia consiste en pensar que ambos trabajan en niveles diferentes.

El Álgebra Relacional constituye un ​**modelo formal**​.

Describe operaciones matemáticas sobre relaciones.

SQL, en cambio, es un ​**lenguaje de implementación**​.

Permite que personas y aplicaciones expresen esas operaciones utilizando una sintaxis más cómoda y cercana al lenguaje natural.

Podríamos establecer la siguiente analogía.

Las partituras musicales representan una obra mediante un lenguaje técnico que cualquier músico puede interpretar.

La música que finalmente escucha el público constituye la ejecución práctica de esa partitura.

De forma parecida, el Álgebra Relacional describe la lógica de una consulta y SQL proporciona un lenguaje práctico para escribirla.

### Un mismo problema, dos representaciones

Supongamos que el responsable comercial desea conocer todos los clientes residentes en Santander.

Desde el punto de vista conceptual el problema consiste en seleccionar determinadas tuplas de la relación ​**Cliente**​.

En Álgebra Relacional utilizaríamos el operador de selección.

En SQL escribiríamos una consulta con la cláusula `WHERE`.

Aunque la sintaxis sea distinta, la intención es exactamente la misma.

En ambos casos estamos filtrando las filas que cumplen una determinada condición.

### Selección y WHERE

La correspondencia más directa aparece entre la operación de selección y la cláusula `WHERE`.

| Álgebra Relacional             | SQL   |
| --------------------------------- | ------- |
| Seleccionar determinadas tuplas | WHERE |

Siempre que una consulta SQL incorpora una condición, el optimizador puede interpretarla como una selección sobre una relación.

Por ello, muchos planes de ejecución muestran esta operación incluso aunque el usuario nunca haya escrito una expresión algebraica.

### Proyección y SELECT

Otro paralelismo muy importante aparece entre la proyección y la cláusula `SELECT`.

En Álgebra Relacional la proyección conserva únicamente determinados atributos.

En SQL, la lista de columnas situada después de la palabra `SELECT` cumple precisamente esa función.

Cuando escribimos:

```sql
SELECT Nombre, CorreoElectronico
FROM Cliente;
```

estamos indicando qué atributos deseamos conservar en el resultado.

Desde el punto de vista algebraico estamos realizando una proyección.

### Varias operaciones en una sola consulta

Una de las diferencias que más sorprenden al comenzar a trabajar con SQL es que una única sentencia puede representar varias operaciones algebraicas consecutivas.

Por ejemplo, una consulta aparentemente sencilla puede implicar:

* seleccionar determinadas tuplas;
* proyectar ciertos atributos;
* combinar varias relaciones;
* ordenar el resultado;
* eliminar duplicados.

El usuario escribe una única sentencia.

El sistema la descompone internamente en numerosas operaciones algebraicas antes de ejecutarla.

### SQL incorpora muchas más funcionalidades

El Álgebra Relacional se centra exclusivamente en describir operaciones sobre relaciones.

SQL va mucho más allá.

Además de consultar información, permite:

* crear bases de datos;
* definir tablas;
* insertar registros;
* modificar datos;
* eliminar información;
* gestionar permisos;
* controlar transacciones;
* crear índices;
* definir vistas.

Por tanto, SQL no sustituye al Álgebra Relacional.

La utiliza como uno de sus fundamentos para las operaciones de consulta.

### El papel del optimizador

Uno de los aspectos más interesantes de los SGBD modernos es que raramente ejecutan una consulta SQL tal y como ha sido escrita.

Después de analizar su sintaxis, el optimizador genera una representación interna basada en operadores algebraicos.

Sobre esa representación aplica numerosas transformaciones.

Puede cambiar el orden de las operaciones.

Puede eliminar pasos innecesarios.

Puede utilizar índices.

Puede reorganizar la consulta para reducir el coste de ejecución.

Finalmente genera un plan que será el que realmente acceda a los datos.

Por este motivo, comprender el Álgebra Relacional ayuda también a comprender cómo trabajan los optimizadores de consultas.

### Nuestro caso de estudio

Imaginemos una consulta que obtenga el nombre de todos los productos cuyo stock sea inferior a diez unidades.

Aunque el usuario únicamente escriba una sentencia SQL, el motor probablemente realizará internamente una secuencia similar a esta:

```text
Producto
      ↓
Selección (Stock < 10)
      ↓
Proyección (Nombre)
      ↓
Resultado
```

Este proceso resulta prácticamente idéntico al razonamiento que hemos desarrollado durante toda esta clase.

### Errores frecuentes

Un error muy común consiste en pensar que SQL ejecuta las cláusulas exactamente en el orden en que aparecen escritas.

En realidad, el optimizador puede reorganizar internamente muchas de esas operaciones sin modificar el resultado final.

También es frecuente creer que aprender Álgebra Relacional deja de tener utilidad una vez dominado SQL.

Ocurre justamente lo contrario: cuanto más complejas son las consultas, mayor utilidad tiene comprender la lógica algebraica que existe detrás de ellas.

### Ideas clave

* Álgebra Relacional y SQL persiguen el mismo objetivo, pero trabajan en niveles diferentes.
* SQL proporciona una sintaxis práctica para expresar operaciones algebraicas.
* Muchas cláusulas de SQL tienen una correspondencia directa con operadores del Álgebra Relacional.
* Los motores relacionales transforman las consultas SQL en expresiones algebraicas antes de ejecutarlas.
* Comprender esta relación facilitará el estudio de consultas SQL complejas y de la optimización de consultas.

