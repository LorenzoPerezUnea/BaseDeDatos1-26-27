# Consultas compuestas

## Introducción

En los capítulos anteriores se ha establecido la correspondencia entre los operadores fundamentales del Álgebra Relacional y las principales cláusulas de SQL. Cada operador se ha estudiado de forma independiente para comprender con claridad cuál es su función y cómo se traduce entre ambos lenguajes.

Sin embargo, las consultas que aparecen en un entorno profesional rara vez utilizan un único operador. Lo habitual es que una misma consulta combine selecciones, proyecciones, uniones entre relaciones y, en ocasiones, operaciones de conjuntos. Resolver un problema real implica construir una secuencia de operaciones que transforman progresivamente la información hasta obtener el resultado deseado.

En este capítulo aprenderemos a interpretar esas consultas compuestas y a reconocer que, aunque la sintaxis de SQL parezca muy distinta, la lógica que existe detrás sigue siendo la misma que en el Álgebra Relacional.

### Una consulta es una secuencia de transformaciones

Cuando un estudiante observa una consulta SQL relativamente larga suele intentar leerla de izquierda a derecha como si fuera una frase escrita en lenguaje natural.

Esta estrategia funciona para consultas muy sencillas, pero deja de ser útil cuando aparecen varias tablas, filtros, agrupaciones o uniones.

El Álgebra Relacional propone una forma diferente de pensar.

Cada operador toma una relación como entrada y produce una nueva relación como salida.

Esa nueva relación puede convertirse, a su vez, en la entrada del siguiente operador.

En consecuencia, una consulta compleja puede entenderse como una cadena de transformaciones sucesivas.

Por ejemplo, supongamos que queremos obtener el nombre de los clientes de Santander que hayan comprado productos de la categoría ​**Monitores**​.

En Álgebra Relacional podemos descomponer el problema en varios pasos.

```text
R1 ← σ Ciudad='Santander' (Cliente)

R2 ← σ Categoria='Monitores' (Producto)

R3 ← R1 ⋈ R1.IdCliente = Pedido.IdCliente Pedido

R4 ← R3 ⋈ Pedido.IdPedido = LineaPedido.IdPedido LineaPedido

R5 ← R4 ⋈ LineaPedido.IdProducto = R2.IdProducto R2

Resultado ← π R1.Nombre (R5)
```

Cada relación intermedia representa un estado del procesamiento.

Esta forma de escribir las consultas resulta especialmente útil para aprender, depurar errores y comprender el funcionamiento del optimizador.

### La misma consulta en SQL

La traducción directa sería:

```sql
SELECT DISTINCT c.Nombre
FROM Cliente c
INNER JOIN Pedido p
    ON c.IdCliente = p.IdCliente
INNER JOIN LineaPedido lp
    ON p.IdPedido = lp.IdPedido
INNER JOIN Producto pr
    ON lp.IdProducto = pr.IdProducto
WHERE c.Ciudad = 'Santander'
  AND pr.Categoria = 'Monitores';
```

Aunque la sintaxis es diferente, ambas consultas siguen exactamente el mismo recorrido lógico:

1. Identificar los clientes de Santander.
2. Identificar los productos de la categoría Monitores.
3. Relacionar clientes con pedidos.
4. Relacionar pedidos con sus líneas.
5. Relacionar las líneas con los productos.
6. Mostrar únicamente el nombre del cliente.

La diferencia es que SQL expresa el problema de forma declarativa, mientras que el Álgebra Relacional lo representa como una composición explícita de operaciones.

### Aprender a "ver" el Álgebra Relacional dentro de SQL

Uno de los objetivos más importantes de esta clase consiste en que el estudiante sea capaz de leer una consulta SQL e identificar inmediatamente qué operadores relacionales están presentes.

Por ejemplo:

```sql
SELECT Nombre
FROM Cliente
WHERE Ciudad = 'Santander';
```

Puede interpretarse mentalmente como:

```text
π Nombre
(
    σ Ciudad='Santander'
    (
        Cliente
    )
)
```

Del mismo modo, una consulta con varias tablas:

```sql
SELECT c.Nombre, p.Fecha
FROM Cliente c
INNER JOIN Pedido p
    ON c.IdCliente = p.IdCliente;
```

Puede entenderse como:

```text
π Nombre, Fecha
(
    Cliente ⋈ Pedido
)
```

Este ejercicio mental permite comprender el funcionamiento de SQL con mucha mayor profundidad que la simple memorización de su sintaxis.

### El orden lógico y el orden de escritura

Otro aspecto que suele generar confusión es que SQL no se escribe en el mismo orden en que conceptualmente se ejecutan las operaciones.

Por ejemplo:

```sql
SELECT
FROM
JOIN
WHERE
```

No significa que el motor procese primero el SELECT y después el FROM.

Internamente, el optimizador reorganiza las operaciones para construir un plan de ejecución eficiente.

Desde el punto de vista conceptual, resulta más cercano al razonamiento del Álgebra Relacional:

1. Seleccionar las relaciones implicadas.
2. Combinar las relaciones necesarias.
3. Aplicar las condiciones de filtrado.
4. Elegir los atributos que formarán parte del resultado.

Esta diferencia explica por qué conocer el Álgebra Relacional facilita tanto la comprensión del comportamiento interno de los SGBD.

### Estrategia para resolver consultas complejas

A medida que las consultas aumentan de tamaño, resulta recomendable seguir siempre una metodología de resolución.

Una estrategia útil consiste en responder, en este orden, a las siguientes preguntas:

1. ¿Qué información debe aparecer en el resultado?
2. ¿En qué relación se encuentra cada dato?
3. ¿Qué relaciones deben combinarse?
4. ¿Qué condiciones limitan el conjunto de resultados?
5. ¿Qué atributos deben proyectarse al final?

Esta secuencia coincide prácticamente con el proceso seguido por un diseñador de bases de datos al construir consultas profesionales.

### Casos reales

En un sistema de gestión empresarial es habitual encontrar consultas que combinan cinco, seis o incluso diez tablas.

Por ejemplo:

* informes de ventas por cliente y período;
* seguimiento completo de un pedido desde su creación hasta el envío;
* historial de compras de un cliente con información de productos, promociones y pagos;
* análisis de inventario relacionando almacenes, proveedores y movimientos de stock.

Aunque estas consultas parezcan muy complejas, todas ellas pueden descomponerse en una sucesión de operaciones relacionales sencillas.

### Errores frecuentes

Un error muy común consiste en escribir consultas SQL directamente, sin haber pensado previamente cuál es el recorrido entre las relaciones.

También es frecuente intentar resolver un problema complejo en un único paso, cuando resulta mucho más sencillo dividirlo en operaciones intermedias.

Por último, muchos estudiantes olvidan que una consulta puede expresarse de distintas formas y que el optimizador del SGBD buscará una estrategia equivalente más eficiente siempre que sea posible.

### Ideas clave

* Las consultas reales combinan varios operadores del Álgebra Relacional.
* Una consulta compleja puede entenderse como una cadena de transformaciones sucesivas.
* SQL y el Álgebra Relacional siguen la misma lógica, aunque utilicen sintaxis diferentes.
* Aprender a identificar los operadores relacionales dentro de una consulta SQL facilita enormemente su comprensión.
* Dividir una consulta en pasos intermedios es una estrategia eficaz tanto para aprender como para depurar errores.
* El razonamiento algebraico constituye la base sobre la que trabajan los optimizadores de consultas de los sistemas gestores de bases de datos.

