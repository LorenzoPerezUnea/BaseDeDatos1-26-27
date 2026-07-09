# Soluciones guiadas — Bloque 3. Operaciones entre conjuntos

## Introducción

En este bloque se estudian tres de los operadores fundamentales del Álgebra Relacional:

* **Unión (∪)**
* **Intersección (∩)**
* **Diferencia (−)**

A diferencia de los bloques anteriores, estas operaciones ​**no combinan relaciones mediante claves**​, sino que trabajan directamente con ​**conjuntos de tuplas**​.

Es importante recordar que estos operadores solo pueden aplicarse entre ​**relaciones compatibles**​, es decir:

* poseen el mismo número de atributos;
* los atributos correspondientes pertenecen a dominios compatibles;
* representan el mismo tipo de información.

En este bloque continuaremos utilizando la notación mediante ​**relaciones intermedias**​, aunque muchas consultas podrían resolverse mediante una única expresión. El objetivo es mantener un estilo uniforme en todo el curso.

---

# Ejercicio 1

### Enunciado

Obtener todos los clientes que pertenezcan al programa **Newsletter** o al programa ​**Premium**​.

### Solución

```text
R1 ← ClientesNewsletter

R2 ← ClientesPremium

R3 ← R1 ∪ R2

Resultado ← R3
```

### Explicación

La unión reúne todas las tuplas presentes en cualquiera de las dos relaciones.

Las tuplas duplicadas aparecen una única vez en el resultado.

---

# Ejercicio 2

### Enunciado

Obtener únicamente los clientes que pertenezcan simultáneamente al programa **Newsletter** y al programa ​**Premium**​.

### Solución

```text
R1 ← ClientesNewsletter

R2 ← ClientesPremium

R3 ← R1 ∩ R2

Resultado ← R3
```

### Explicación

La intersección conserva únicamente las tuplas comunes a ambas relaciones.

---

# Ejercicio 3

### Enunciado

Obtener los clientes suscritos al boletín que todavía no pertenecen al programa ​**Premium**​.

### Solución

```text
R1 ← ClientesNewsletter

R2 ← ClientesPremium

R3 ← R1 − R2

Resultado ← R3
```

### Explicación

La diferencia elimina del primer conjunto todas las tuplas que también aparecen en el segundo.

Debe recordarse que:

```text
A − B ≠ B − A
```

La diferencia ​**no es conmutativa**​.

---

# Ejercicio 4

### Enunciado

La empresa desea obtener todos los productos incluidos en la promoción de **Verano** o en la promoción de ​**Invierno**​.

### Solución

```text
R1 ← ProductosPromocionVerano

R2 ← ProductosPromocionInvierno

R3 ← R1 ∪ R2

Resultado ← R3
```

### Explicación

El resultado contiene todos los productos presentes en cualquiera de las promociones.

---

# Ejercicio 5

### Enunciado

Obtener únicamente los productos que aparecen tanto en la promoción de Verano como en la de Invierno.

### Solución

```text
R1 ← ProductosPromocionVerano

R2 ← ProductosPromocionInvierno

R3 ← R1 ∩ R2

Resultado ← R3
```

### Explicación

Solo permanecerán los productos comunes a ambas promociones.

---

# Ejercicio 6

### Enunciado

Obtener los productos exclusivos de la promoción de Verano.

### Solución

```text
R1 ← ProductosPromocionVerano

R2 ← ProductosPromocionInvierno

R3 ← R1 − R2

Resultado ← R3
```

### Explicación

El resultado contiene únicamente los productos que aparecen en la promoción de Verano y no aparecen en la de Invierno.

---

# Ejercicio 7

### Enunciado

Explica por qué las relaciones utilizadas en una unión deben ser compatibles.

### Solución

Supongamos las siguientes relaciones:

```text
R1 ← ClientesNewsletter

R2 ← ClientesPremium
```

La operación es válida porque ambas poseen exactamente el mismo esquema.

```text
R3 ← R1 ∪ R2

Resultado ← R3
```

En cambio, la siguiente operación sería incorrecta:

```text
Cliente ∪ Producto
```

### Explicación

Las relaciones representan entidades completamente distintas y sus atributos no son compatibles.

La compatibilidad estructural es un requisito imprescindible para aplicar unión, intersección y diferencia.

---

# Ejercicio 8

### Enunciado

¿Sería correcto realizar una unión entre las relaciones **Cliente** y ​**Producto**​?

### Solución

No.

La operación no puede realizarse.

```text
R1 ← Cliente

R2 ← Producto

R3 ← R1 ∪ R2

✗ Operación inválida
```

### Explicación

Aunque ambas sean relaciones, poseen atributos diferentes y representan conceptos distintos del modelo de datos.

---

# Ejercicio 9

### Enunciado

Sean los conjuntos:

A = {1,2,3,4}

B = {3,4,5}

Calcular:

* A ∪ B
* A ∩ B
* A − B
* B − A

### Solución

```text
R1 ← A ∪ B

Resultado ← {1,2,3,4,5}
```

```text
R2 ← A ∩ B

Resultado ← {3,4}
```

```text
R3 ← A − B

Resultado ← {1,2}
```

```text
R4 ← B − A

Resultado ← {5}
```

### Explicación

Aunque se trabaja con conjuntos matemáticos y no con relaciones, el comportamiento de los operadores es exactamente el mismo.

---

# Ejercicio 10

### Enunciado

Una empresa dispone de dos almacenes.

Indicar el operador adecuado para responder a cada consulta.

### Solución

| Consulta                                           | Operador |
| ---------------------------------------------------- | ---------- |
| Productos presentes en cualquiera de los almacenes | ∪       |
| Productos presentes en ambos almacenes             | ∩       |
| Productos exclusivos del almacén A                | −       |
| Productos exclusivos del almacén B                | −       |

### Explicación

La resolución consiste en identificar correctamente la operación de teoría de conjuntos asociada al enunciado.

No es necesario construir expresiones algebraicas más complejas.

---

# Ejercicio 11

### Enunciado

Indicar si las siguientes afirmaciones son verdaderas o falsas.

### Solución

| Afirmación                                                 |      Respuesta      | Justificación                                 |
| ------------------------------------------------------------- | :-------------------: | ------------------------------------------------ |
| La unión elimina duplicados.                               | **Verdadero** | El resultado sigue siendo una relación.       |
| La diferencia es conmutativa.                               |   **Falso**   | El orden modifica el resultado.                |
| La intersección obtiene únicamente los elementos comunes. | **Verdadero** | Es la definición del operador.                |
| El orden de los operandos no afecta a la diferencia.        |   **Falso**   | A − B y B − A producen resultados distintos. |

### Explicación

Este ejercicio evalúa la comprensión conceptual de los operadores más que la capacidad de escribir expresiones algebraicas.

---

# Ejercicio 12

### Enunciado

La empresa desea obtener el listado de clientes registrados que todavía no han realizado ningún pedido.

### Solución

Primero se obtiene el conjunto de identificadores de todos los clientes.

```text
R1 ← π IdCliente (Cliente)
```

Después se obtiene el conjunto de identificadores presentes en los pedidos.

```text
R2 ← π IdCliente (Pedido)
```

Se calcula la diferencia.

```text
R3 ← R1 − R2
```

Finalmente se recuperan los nombres de dichos clientes.

```text
R4 ← R3 ⋈ R3.IdCliente = Cliente.IdCliente Cliente

R5 ← π Nombre (R4)

Resultado ← R5
```

### Explicación

Este ejercicio es especialmente interesante porque combina operadores de conjuntos con un JOIN.

El operador diferencia permite identificar qué clientes no aparecen en la relación Pedido.

Posteriormente, el JOIN recupera la información descriptiva asociada a esos identificadores.

---

# Observaciones para la corrección

Los errores más frecuentes son:

* confundir la diferencia con una selección mediante desigualdad;
* creer que la diferencia es conmutativa;
* intentar aplicar operaciones entre relaciones incompatibles;
* olvidar que la unión elimina automáticamente las tuplas duplicadas;
* utilizar JOIN cuando el problema únicamente requiere comparar conjuntos.

Una buena estrategia consiste en pedir al estudiante que identifique primero la palabra clave del enunciado:

* **"o"** → Unión (∪)
* **"y"** → Intersección (∩)
* ​**"pero no"**​, ​**"excepto"**​, **"sin"** → Diferencia (−)

Esta asociación ayuda a seleccionar rápidamente el operador adecuado antes de comenzar a construir la consulta.

