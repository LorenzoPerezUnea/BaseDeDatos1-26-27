# Equivalencia con SQL

## Introducción

Hasta este momento hemos trabajado casi exclusivamente con el Álgebra Relacional.

Hemos estudiado sus operadores, su notación y la forma de combinar operaciones para resolver distintos problemas.

Sin embargo, la mayoría de los profesionales no escriben expresiones algebraicas durante su trabajo diario.

Utilizan SQL.

Entonces surge una pregunta natural.

> **¿Cómo se relaciona todo lo aprendido con el lenguaje que realmente utilizaremos?**

La respuesta es sencilla.

Prácticamente todas las consultas SQL pueden interpretarse como una combinación de operadores del Álgebra Relacional.

SQL no reemplaza al Álgebra Relacional.

La implementa.

---

### Una traducción conceptual

El siguiente cuadro resume las equivalencias más importantes.

| Álgebra Relacional      | SQL                         |
| -------------------------- | ----------------------------- |
| Selección (σ)          | WHERE                       |
| Proyección (π)         | Lista de columnas en SELECT |
| Producto cartesiano (×) | CROSS JOIN                  |
| Unión (∪)              | UNION                       |
| Intersección (∩)       | INTERSECT                   |
| Diferencia (−)          | EXCEPT / MINUS              |
| Renombramiento (ρ)      | Alias (AS)                  |
| JOIN derivado            | INNER JOIN y variantes      |

No se trata de una traducción literal.

Se trata de una correspondencia conceptual.

---

### Ejemplo 1

Problema:

> Obtener el nombre y el precio de los productos cuyo stock sea inferior a diez unidades.

Desde el punto de vista algebraico el razonamiento es:

1. Selección.
2. Proyección.

En SQL escribiríamos:

```sql
SELECT Nombre, Precio
FROM Producto
WHERE Stock < 10;
```

Aunque la sintaxis sea distinta, ambas expresiones describen exactamente el mismo proceso.

---

### Ejemplo 2

Problema:

> Obtener el nombre de los clientes que realizaron algún pedido.

Conceptualmente:

1. JOIN.
2. Proyección.

En SQL:

```sql
SELECT c.Nombre
FROM Cliente c
INNER JOIN Pedido p
ON c.IdCliente = p.IdCliente;
```

El Álgebra Relacional nos ayuda a comprender por qué la consulta necesita combinar ambas relaciones antes de poder obtener el resultado.

---

### El orden aparente y el orden real

Una de las diferencias que más confunden a los principiantes es el orden en que se escribe SQL.

Visualmente solemos escribir:

```sql
SELECT
FROM
JOIN
WHERE
GROUP BY
HAVING
ORDER BY
```

Sin embargo, internamente el sistema no sigue necesariamente esa secuencia.

Primero construye una representación algebraica.

Después reorganiza las operaciones buscando el menor coste posible.

Por esta razón comprender el Álgebra Relacional resulta tan útil incluso cuando trabajamos exclusivamente con SQL.

---

### SQL incorpora muchas más capacidades

El Álgebra Relacional está orientada únicamente a la recuperación de información.

SQL, por el contrario, constituye un lenguaje mucho más amplio.

Además de consultar datos permite:

* crear tablas;
* insertar registros;
* modificar información;
* eliminar datos;
* gestionar usuarios;
* controlar transacciones;
* definir vistas;
* crear índices.

Por tanto, el Álgebra Relacional representa únicamente una parte de todo lo que SQL puede hacer.

No obstante, es probablemente la parte más importante para comprender las consultas.

---

### Aplicación al caso de estudio

Durante las próximas clases todas las consultas SQL que escribamos podrán analizarse desde dos perspectivas.

La primera será la sintaxis del lenguaje.

La segunda será el razonamiento algebraico que existe detrás.

Con el tiempo descubrirás que pensar primero en Álgebra Relacional facilita mucho la construcción de consultas SQL correctas.

Esta estrategia también ayuda a detectar errores antes incluso de ejecutar una consulta.

---

### Errores frecuentes

Muchos estudiantes intentan memorizar la sintaxis SQL sin comprender qué operación representa cada cláusula.

Como consecuencia escriben consultas que funcionan por ensayo y error.

Comprender la equivalencia con el Álgebra Relacional permite construir consultas de forma mucho más razonada.

---

### Ideas clave

* SQL implementa muchas de las operaciones definidas por el Álgebra Relacional.
* Existe una correspondencia conceptual entre la mayoría de los operadores algebraicos y las cláusulas de SQL.
* Una consulta SQL puede interpretarse como una secuencia de operaciones algebraicas.
* El optimizador trabaja precisamente sobre esa representación interna.
* Pensar primero en términos algebraicos facilita el aprendizaje de SQL y la construcción de consultas correctas.

