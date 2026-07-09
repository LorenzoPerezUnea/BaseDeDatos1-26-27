# WHERE como selección

## Introducción

Si la proyección responde a la pregunta ​**"¿qué columnas quiero mostrar?"**​, la selección responde a una pregunta completamente diferente:

> **¿Qué filas cumplen las condiciones de la consulta?**

En Álgebra Relacional esta operación se representa mediante el operador ​**σ (sigma)**​.

En SQL, la misma idea aparece implementada mediante la cláusula ​**WHERE**​.

Comprender esta correspondencia resulta esencial porque la inmensa mayoría de las consultas profesionales utilizan algún tipo de filtrado.

Sin selección, una consulta devuelve normalmente todas las filas de una tabla.

En cambio, la mayoría de los problemas reales consisten precisamente en localizar un subconjunto concreto de la información almacenada.

### La selección en Álgebra Relacional

La forma general es:

```text
σ condición (Relación)
```

Por ejemplo:

```text
σ Ciudad='Santander' (Cliente)
```

La consulta conserva únicamente las tuplas cuya ciudad sea Santander.

Es importante observar que la estructura de la relación permanece exactamente igual.

No desaparecen columnas.

Únicamente desaparecen filas.

### La misma consulta en SQL

La traducción directa es:

```sql
SELECT *
FROM Cliente
WHERE Ciudad='Santander';
```

La correspondencia puede resumirse así:

| Álgebra Relacional | SQL        |
| --------------------- | ------------ |
| σ                  | WHERE      |
| condición          | condición |
| Relación           | FROM       |

SQL separa la operación en distintas cláusulas, mientras que el Álgebra Relacional la representa mediante un único operador.

Conceptualmente ambas expresiones describen exactamente el mismo proceso.

### Combinación de condiciones

Al igual que ocurría en el Álgebra Relacional, SQL permite combinar varias condiciones mediante operadores lógicos.

Por ejemplo, para obtener los productos de la categoría Monitores cuyo precio sea superior a 300 €:

Álgebra Relacional:

```text
σ Categoria='Monitores'
∧ Precio>300
(
Producto
)
```

SQL:

```sql
SELECT *
FROM Producto
WHERE Categoria='Monitores'
  AND Precio>300;
```

La estructura lógica permanece idéntica.

Únicamente cambia la sintaxis utilizada para expresarla.

### Selección antes de combinar relaciones

Durante la clase anterior se insistió en una regla de optimización muy importante:

Siempre que sea posible, las selecciones deben aplicarse antes de realizar los JOIN.

Esta idea también aparece posteriormente en SQL.

Aunque el desarrollador escriba una consulta completa, el optimizador del SGBD intentará ejecutar primero aquellos filtros que reduzcan el volumen de datos.

Por tanto, comprender la selección desde el Álgebra Relacional ayuda también a comprender cómo funcionan internamente los optimizadores de consultas.

### Errores frecuentes

Muchos estudiantes confunden SELECT y WHERE porque ambos parecen "seleccionar" información.

En realidad realizan tareas completamente distintas.

SELECT decide qué columnas aparecen.

WHERE decide qué filas permanecen.

Otra confusión habitual consiste en pensar que WHERE modifica la tabla.

No es así.

La selección construye un resultado temporal.

La información almacenada en la base de datos permanece inalterada.

### Ideas clave

* La selección (σ) corresponde a la cláusula WHERE.
* WHERE filtra filas; SELECT elige columnas.
* La estructura de la relación no cambia durante una selección.
* Las condiciones pueden combinarse mediante operadores lógicos.
* Aplicar las selecciones cuanto antes mejora normalmente el rendimiento de las consultas.

