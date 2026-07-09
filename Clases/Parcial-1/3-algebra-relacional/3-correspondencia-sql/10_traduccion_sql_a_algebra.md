# Traducción de SQL a Álgebra Relacional

## Introducción

Aprender a traducir consultas desde el Álgebra Relacional hacia SQL resulta imprescindible para escribir consultas correctamente. Sin embargo, el proceso inverso posee un valor didáctico incluso mayor.

Cuando un estudiante es capaz de leer una sentencia SQL y expresar la misma consulta mediante Álgebra Relacional, demuestra que ha comprendido la lógica del Modelo Relacional y que ya no depende únicamente de memorizar palabras reservadas.

Esta capacidad será especialmente útil durante el resto del curso. A partir de las próximas clases comenzaremos a trabajar directamente con MySQL y utilizaremos SQL de forma continua. Poder visualizar mentalmente la expresión algebraica que existe detrás de cada consulta ayudará a comprender mejor tanto el funcionamiento del lenguaje como las decisiones tomadas por el optimizador del sistema gestor.

### Método de traducción

La traducción desde SQL hacia el Álgebra Relacional puede realizarse siguiendo siempre el mismo procedimiento.

1. Identificar las relaciones utilizadas en la cláusula `FROM`.
2. Analizar cómo se combinan mediante los distintos `JOIN`.
3. Extraer las condiciones de filtrado presentes en `WHERE`.
4. Identificar los atributos proyectados en `SELECT`.
5. Expresar las operaciones siguiendo la notación del Álgebra Relacional.

Este orden coincide con la construcción lógica de la consulta, aunque no necesariamente con el orden en que aparece escrita en SQL.

### Ejemplo 1. Consulta sencilla

Consideremos la siguiente consulta.

```sql
SELECT Nombre
FROM Cliente
WHERE Ciudad = 'Santander';
```

Las relaciones utilizadas son:

* Cliente.

El filtro es:

* Ciudad = 'Santander'.

El resultado solicitado es:

* Nombre.

La expresión equivalente en Álgebra Relacional es:

```text
π Nombre
(
    σ Ciudad='Santander'
    (
        Cliente
    )
)
```

La consulta mantiene exactamente el mismo significado.

### Ejemplo 2. Consulta con JOIN

Supongamos ahora la siguiente sentencia SQL.

```sql
SELECT c.Nombre,
       p.Fecha
FROM Cliente c
INNER JOIN Pedido p
    ON c.IdCliente = p.IdCliente;
```

El recorrido entre las relaciones es:

Cliente → Pedido

La expresión algebraica correspondiente puede escribirse como:

```text
π Nombre, Fecha
(
    Cliente
    ⋈ Cliente.IdCliente = Pedido.IdCliente
    Pedido
)
```

También podría expresarse utilizando únicamente operadores fundamentales:

```text
π Nombre, Fecha
(
    σ Cliente.IdCliente = Pedido.IdCliente
    (
        Cliente × Pedido
    )
)
```

Ambas expresiones son equivalentes, aunque la primera resulta mucho más compacta y legible.

### Ejemplo 3. Consulta con varias condiciones

Veamos una consulta ligeramente más compleja.

```sql
SELECT Nombre
FROM Producto
WHERE Categoria = 'Monitores'
  AND Precio > 300;
```

La traducción es:

```text
π Nombre
(
    σ Categoria='Monitores'
      ∧ Precio>300
    (
        Producto
    )
)
```

En este caso puede observarse que la cláusula `WHERE` se convierte directamente en la condición de la selección.

### Casos reales

Durante el diseño de una base de datos es habitual que las consultas se describan inicialmente mediante diagramas o expresiones algebraicas sencillas antes de implementarse en SQL.

Esta práctica ayuda a separar el razonamiento lógico de los detalles sintácticos del lenguaje utilizado por el sistema gestor.

### Errores frecuentes

Uno de los errores más habituales consiste en copiar el orden de las cláusulas SQL dentro de la expresión algebraica.

Otro error frecuente es olvidar que la proyección es normalmente la operación más externa de la expresión, mientras que las selecciones y uniones aparecen en niveles inferiores.

También es común confundir un `JOIN` con un simple producto cartesiano, ignorando la condición que relaciona ambas tablas.

### Ideas clave

* Traducir SQL a Álgebra Relacional permite comprender la lógica que existe detrás de una consulta.
* El proceso comienza identificando las relaciones y termina con la proyección final.
* Un `JOIN` puede expresarse mediante el operador de unión o mediante un producto cartesiano seguido de una selección.
* La traducción favorece el razonamiento lógico y facilita el aprendizaje de consultas complejas.
* Dominar ambos sentidos de traducción constituye una excelente preparación para el trabajo práctico con MySQL.

