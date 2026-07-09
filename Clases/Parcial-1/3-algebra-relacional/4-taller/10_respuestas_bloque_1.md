# Soluciones guiadas — Bloque 1. Selección y proyección

## Introducción

En este primer bloque todas las consultas pueden resolverse utilizando únicamente los operadores **selección (σ)** y ​**proyección (π)**​.

El objetivo es que el estudiante aprenda a distinguir claramente entre:

* ​**seleccionar tuplas**​, es decir, filtrar filas según una condición;
* ​**proyectar atributos**​, es decir, conservar únicamente las columnas necesarias.

A partir de este solucionario se utilizará como **notación recomendada del curso** la resolución paso a paso mediante **relaciones intermedias** (`R1`, `R2`, `R3`, ...).

Aunque las expresiones completamente anidadas son formalmente correctas y aparecen habitualmente en los libros de teoría, el formato mediante variables presenta importantes ventajas didácticas:

* facilita la lectura;
* permite detectar errores con mayor facilidad;
* favorece la asignación de puntuación parcial;
* aproxima el razonamiento al funcionamiento interno de los optimizadores de consultas.

---

# Ejercicio 1

### Enunciado

Obtener **todos los datos** de los clientes cuya ciudad sea ​**Santander**​.

### Solución

```text
R1 ← σ Ciudad='Santander' (Cliente)

Resultado ← R1
```

### Explicación

La consulta únicamente requiere una selección.

No es necesaria ninguna proyección porque el enunciado solicita todos los atributos de la relación.

---

# Ejercicio 2

### Enunciado

Obtener únicamente el **nombre** de todos los clientes.

### Solución

```text
R1 ← π Nombre (Cliente)

Resultado ← R1
```

### Explicación

No existe ningún filtrado.

La operación consiste exclusivamente en proyectar el atributo solicitado.

---

# Ejercicio 3

### Enunciado

Obtener el **nombre** y la **ciudad** de los clientes de Bilbao.

### Solución

```text
R1 ← σ Ciudad='Bilbao' (Cliente)

R2 ← π Nombre, Ciudad (R1)

Resultado ← R2
```

### Explicación

Siempre que sea posible se recomienda realizar primero la selección y posteriormente la proyección.

De este modo únicamente se proyectan las tuplas que realmente formarán parte del resultado.

---

# Ejercicio 4

### Enunciado

Mostrar todos los productos cuyo precio sea superior a 200 €.

### Solución

```text
R1 ← σ Precio > 200 (Producto)

Resultado ← R1
```

### Explicación

Como deben mostrarse todos los atributos del producto, únicamente es necesaria una selección.

---

# Ejercicio 5

### Enunciado

Obtener únicamente el **nombre** de todos los productos pertenecientes a la categoría ​**Periféricos**​.

### Solución

```text
R1 ← σ Categoria='Periféricos' (Producto)

R2 ← π Nombre (R1)

Resultado ← R2
```

### Explicación

Primero se identifican los productos de la categoría indicada y después se conserva únicamente el atributo solicitado.

---

# Ejercicio 6

### Enunciado

Mostrar el nombre y el precio de todos los productos cuyo precio sea inferior a 100 €.

### Solución

```text
R1 ← σ Precio < 100 (Producto)

R2 ← π Nombre, Precio (R1)

Resultado ← R2
```

### Explicación

La proyección elimina todos los atributos que no son necesarios para responder a la consulta.

---

# Ejercicio 7

### Enunciado

Obtener el listado de categorías existentes en el catálogo de productos.

### Solución

```text
R1 ← π Categoria (Producto)

Resultado ← R1
```

### Explicación

La proyección elimina automáticamente las categorías repetidas, ya que una relación no puede contener tuplas duplicadas.

---

# Ejercicio 8

### Enunciado

Mostrar todos los clientes excepto aquellos que viven en Santander.

### Solución

```text
R1 ← σ Ciudad ≠ 'Santander' (Cliente)

Resultado ← R1
```

### Explicación

Aunque podría utilizarse el operador diferencia, la selección resulta mucho más directa y eficiente para este problema.

---

# Ejercicio 9

### Enunciado

Obtener el nombre de los productos cuyo precio esté comprendido entre 50 € y 200 €.

### Solución

```text
R1 ← σ Precio ≥ 50 ∧ Precio ≤ 200 (Producto)

R2 ← π Nombre (R1)

Resultado ← R2
```

### Explicación

Las dos condiciones se combinan mediante el operador lógico AND (∧).

---

# Ejercicio 10

### Enunciado

Mostrar únicamente los nombres de los clientes cuyo nombre comience por la letra ​**L**​.

### Solución

```text
R1 ← σ Nombre LIKE 'L%' (Cliente)

R2 ← π Nombre (R1)

Resultado ← R2
```

### Explicación

En Álgebra Relacional clásica no existe una sintaxis estándar para búsquedas mediante patrones de texto.

En este curso se admite la notación **LIKE** como extensión didáctica para facilitar la transición posterior a SQL.

---

# Ejercicio 11

### Enunciado

Obtener el identificador y el nombre de todos los productos pertenecientes a la categoría **Periféricos** cuyo precio sea inferior a 80 €.

### Solución

```text
R1 ← σ Categoria='Periféricos' ∧ Precio < 80 (Producto)

R2 ← π IdProducto, Nombre (R1)

Resultado ← R2
```

### Explicación

Las dos condiciones pueden expresarse mediante una única selección, evitando operaciones innecesarias.

---

# Ejercicio 12

### Enunciado

La dirección comercial desea elaborar un listado con los nombres de los clientes de Santander.

Explica brevemente por qué resulta más eficiente proyectar únicamente el atributo **Nombre** que devolver la relación completa ​**Cliente**​.

### Solución

```text
R1 ← σ Ciudad='Santander' (Cliente)

R2 ← π Nombre (R1)

Resultado ← R2
```

### Explicación

La proyección reduce el número de atributos transportados durante la consulta.

Esto produce varias ventajas:

* disminuye el volumen de datos procesado;
* simplifica el resultado devuelto al usuario;
* reduce el consumo de memoria;
* facilita el procesamiento de las operaciones posteriores.

En general, una consulta debe devolver únicamente la información que realmente ha solicitado el usuario.

---

# Observaciones para la corrección

Los errores más habituales en este bloque son:

* confundir selección y proyección;
* proyectar antes de seleccionar cuando ello elimina atributos necesarios para evaluar la condición;
* olvidar la proyección cuando el enunciado solicita únicamente algunos atributos;
* utilizar operadores innecesarios para resolver consultas sencillas;
* escribir condiciones de selección incompletas o incorrectas.

Durante la corrección conviene insistir en que el estudiante piense siempre en dos preguntas antes de escribir una consulta:

1. **¿Qué filas necesito conservar?** → Selección (σ).
2. **¿Qué columnas debo mostrar?** → Proyección (π).

Responder correctamente a estas dos preguntas suele ser suficiente para resolver la mayoría de las consultas básicas de Álgebra Relacional.

