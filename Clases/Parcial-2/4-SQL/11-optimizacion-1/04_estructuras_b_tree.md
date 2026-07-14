# Estructuras B-Tree

## Introducción

En el apartado anterior aprendimos que un índice permite localizar registros de forma mucho más rápida que recorriendo una tabla completa.

La siguiente pregunta es inmediata:

> ¿Cómo consigue un índice encontrar un registro entre millones de filas en apenas unas pocas operaciones?

La respuesta está en la estructura de datos utilizada para almacenar los índices.

En MySQL, cuando trabajamos con el motor **InnoDB**, la mayoría de los índices se implementan mediante una estructura denominada **B-Tree** (más concretamente, una variante conocida como **B+Tree**).

No es necesario convertirse en especialista en estructuras de datos para utilizar índices correctamente, pero comprender cómo funcionan internamente ayuda a entender por qué ciertas consultas son rápidas y otras no.

## ¿Por qué no sirve una lista?

Imaginemos una tabla con un millón de clientes.

Si los registros estuvieran simplemente almacenados uno detrás de otro, buscar un cliente concreto podría requerir revisar una enorme cantidad de filas.

Conceptualmente tendríamos algo parecido a esto:

```text
1

↓

2

↓

3

↓

4

↓

...

↓

1 000 000
```

En el peor caso habría que recorrer prácticamente toda la lista.

El tiempo de búsqueda crecería proporcionalmente al número de registros.

## Una idea mejor

Ahora imaginemos un árbol.

En lugar de revisar todos los registros, primero decidimos si debemos ir hacia la izquierda o hacia la derecha.

Después repetimos el proceso.

Cada decisión elimina una gran cantidad de posibilidades.

Por ejemplo:

```text
500

       /       \

    250         750

   /   \       /   \

125 375    625   875
```

Si buscamos el valor:

```
625
```

No revisamos todos los números.

Únicamente seguimos un camino.

## ¿Qué es un B-Tree?

Un B-Tree es una estructura jerárquica formada por nodos.

Cada nodo contiene:

- Valores ordenados.
- Referencias a otros nodos.
- Información necesaria para continuar la búsqueda.

En lugar de almacenar un único valor por nodo, como ocurre en un árbol binario clásico, cada nodo almacena muchos valores.

Esto reduce considerablemente la altura del árbol.

## Un ejemplo simplificado

Supongamos el siguiente índice.

```text
[40 | 80]

            /       |       \

      [10 20]   [50 60]   [90 95]
```

Queremos buscar:

```
60
```

Primero observamos el nodo raíz.

```
60 > 40
```

pero

```
60 < 80
```

Por tanto seguimos únicamente la rama central.

Llegamos al nodo:

```
50 60
```

Y encontramos inmediatamente el valor buscado.

Solo hemos necesitado dos niveles.

## ¿Por qué resulta tan eficiente?

Cada nodo almacena muchos valores.

Eso significa que un único paso descarta miles o millones de registros.

En un árbol muy grande la altura sigue siendo pequeña.

Por ejemplo, un índice con millones de registros puede requerir únicamente tres o cuatro accesos para localizar un valor.

Este comportamiento explica por qué las búsquedas mediante índices son tan rápidas.

## B-Tree frente a recorrido completo

Supongamos una tabla con diez millones de filas.

Sin índice.

```text
Fila 1

Fila 2

Fila 3

...

Fila 10 000 000
```

Con índice.

```text
Raíz

↓

Nodo intermedio

↓

Nodo hoja

↓

Registro encontrado
```

En lugar de leer millones de filas, MySQL sigue únicamente un pequeño camino dentro del árbol.

## ¿Qué almacenan las hojas?

En InnoDB los nodos hoja contienen la información necesaria para localizar los registros.

En el índice de la clave primaria, las hojas almacenan directamente las filas de la tabla.

En los índices secundarios, las hojas contienen:

- El valor indexado.
- La clave primaria correspondiente.

Después InnoDB utiliza esa clave primaria para localizar el registro completo.

Este diseño evita duplicar toda la información en cada índice.

## Inserciones

Los árboles no solo permiten búsquedas rápidas.

También facilitan insertar nuevos valores.

Cuando añadimos un registro:

```sql
INSERT INTO Producto ...
```

MySQL busca la posición adecuada dentro del árbol.

Si un nodo queda demasiado lleno, se divide en dos.

Este proceso mantiene el árbol equilibrado.

## Eliminaciones

Cuando se elimina un registro:

```sql
DELETE FROM Producto
WHERE IdProducto = 200;
```

El árbol también se reorganiza si resulta necesario.

Todo este trabajo se realiza automáticamente.

El usuario nunca necesita reorganizar manualmente el árbol.

## Actualizaciones

Modificar una columna indexada implica actualizar también el árbol correspondiente.

Por ejemplo:

```sql
UPDATE Cliente
SET Ciudad = 'Bilbao'
WHERE IdCliente = 250;
```

Si `Ciudad` posee un índice, será necesario modificar esa estructura además de la fila de la tabla.

Por este motivo demasiados índices pueden ralentizar las operaciones de escritura.

## ¿Por qué no utilizar otro tipo de estructura?

Existen otras estructuras de datos muy eficientes.

Por ejemplo:

- Tablas hash.
- Árboles AVL.
- Árboles rojo-negro.
- Trie.
- Skip Lists.

Sin embargo, el B-Tree ofrece un excelente equilibrio entre:

- Búsquedas.
- Inserciones.
- Eliminaciones.
- Ordenación.
- Acceso eficiente desde disco.

Por ello es la estructura elegida por la mayoría de los sistemas gestores de bases de datos relacionales.

## ¿Qué operaciones aprovechan un B-Tree?

Los índices B-Tree son especialmente eficaces para:

```sql
=
```

```sql
<
```

```sql
>
```

```sql
<=
```

```sql
>=
```

```sql
BETWEEN
```

```sql
ORDER BY
```

```sql
GROUP BY
```

También pueden utilizarse en muchas búsquedas mediante prefijos.

Por ejemplo:

```sql
WHERE Nombre LIKE 'Mar%'
```

Sin embargo, no suelen ser útiles para patrones como:

```sql
LIKE '%Mar%'
```

porque el árbol está organizado desde el comienzo del valor.

## Buenas prácticas

- Comprender que un índice no es simplemente una lista ordenada.
- Evitar modificar continuamente columnas muy indexadas.
- Recordar que los índices ocupan espacio adicional.
- Diseñar los índices pensando en las consultas más frecuentes.
- Aprovechar la eficiencia del B-Tree para búsquedas y ordenaciones.

## Conclusiones

La estructura B-Tree permite que MySQL localice registros en muy pocos accesos incluso cuando las tablas contienen millones de filas. Su organización jerárquica, equilibrada y optimizada para el acceso a disco convierte a esta estructura en la base de la mayoría de los índices utilizados por InnoDB.

## Ideas clave

- Los índices de InnoDB se implementan mediante B-Tree (B+Tree).
- El árbol permanece equilibrado automáticamente.
- La altura del árbol es muy pequeña incluso con grandes volúmenes de datos.
- Las búsquedas requieren muy pocos accesos.
- Las inserciones y eliminaciones reorganizan automáticamente el árbol cuando es necesario.

