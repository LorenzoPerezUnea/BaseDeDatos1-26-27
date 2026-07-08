# Selección (σ)

## Introducción

Si tuviéramos que elegir un único operador como el más utilizado de todo el Álgebra Relacional, probablemente sería la ​**selección**​.

Prácticamente todas las consultas reales contienen algún tipo de filtro.

En una empresa es muy poco frecuente querer trabajar con todos los clientes, todos los pedidos o todos los productos al mismo tiempo.

Normalmente buscamos únicamente aquellos datos que cumplen determinadas condiciones.

El operador de selección fue diseñado precisamente para resolver este problema.

Su función consiste en ​**filtrar las tuplas de una relación**​, conservando únicamente aquellas que satisfacen un criterio determinado.

Aunque esta idea resulte sencilla, constituye uno de los pilares sobre los que se construyen consultas mucho más complejas.

---

### La intuición

Imaginemos un archivador con miles de fichas de clientes.

El director comercial nos dice:

> «Necesito únicamente los clientes que viven en Santander.»

No nos pide reorganizar el archivador.

No nos pide modificar la información.

Simplemente quiere trabajar con un subconjunto de los clientes existentes.

Eso es exactamente lo que hace la selección.

Toma una relación y devuelve otra relación que contiene únicamente las tuplas que cumplen una condición.

---

### Definición formal

La selección se representa mediante la letra griega **sigma** (σ).

Su forma general es:

```text
σ condición (Relación)
```

Donde:

* **σ** representa el operador de selección.
* **condición** indica el criterio que debe cumplir cada tupla.
* **Relación** es el conjunto de datos sobre el que se aplica la operación.

El resultado siempre es otra relación con la misma estructura que la original.

---

### ¿Qué cambia y qué permanece?

Una de las características más importantes de la selección es que ​**no modifica la estructura de la relación**​.

Los atributos siguen siendo exactamente los mismos.

Lo único que cambia es el número de tuplas.

Podemos resumir su comportamiento así:

| Elemento                | ¿Cambia? |
| ------------------------- | ----------- |
| Número de atributos    | No        |
| Nombre de los atributos | No        |
| Dominios                | No        |
| Número de tuplas       | Sí       |

Esta propiedad permite combinar posteriormente la selección con otros operadores como la proyección.

---

### Aplicación al caso de estudio

Consideremos la relación ​**Producto**​.

| IdProducto | Nombre              | Precio | Stock |
| -----------: | --------------------- | -------: | ------: |
|        101 | Monitor 27"         | 249,90 |    18 |
|        102 | Ratón Inalámbrico |  34,50 |     6 |
|        103 | Teclado Mecánico   |  89,95 |    42 |
|        104 | Webcam HD           |  79,95 |     4 |

El responsable del almacén desea conocer únicamente los productos cuyo stock sea inferior a diez unidades.

Conceptualmente realizamos una selección.

La nueva relación estará formada únicamente por:

* Ratón Inalámbrico
* Webcam HD

La relación **Producto** permanece exactamente igual.

---

### Condiciones de selección

Las condiciones pueden utilizar distintos operadores de comparación.

Entre los más habituales encontramos:

| Operador | Significado   |
| ---------- | --------------- |
| =        | Igual que     |
| <>       | Distinto de   |
| <        | Menor que     |
| <=       | Menor o igual |
| >        | Mayor que     |
| >=       | Mayor o igual |

Además, las condiciones pueden combinarse mediante operadores lógicos como AND, OR y NOT, exactamente igual que ocurrirá más adelante en SQL.

---

### Selección como filtro

Una buena forma de imaginar este operador consiste en pensar en un filtro.

```mermaid
flowchart LR

A[Todas las tuplas]
-->B[σ Condición]
-->C[Tuplas que cumplen la condición]
```

Las tuplas que no satisfacen la condición simplemente no forman parte del resultado.

No son modificadas.

No son eliminadas de la base de datos.

Únicamente quedan fuera de la nueva relación generada.

---

### Relación con SQL

Cuando estudiemos SQL descubriremos que prácticamente cualquier cláusula `WHERE` representa una selección.

Por ejemplo, una consulta que busque los productos con stock inferior a diez unidades será interpretada internamente por el optimizador como una operación de selección aplicada sobre la relación ​**Producto**​.

En consecuencia, comprender este operador significa comprender uno de los componentes fundamentales de SQL.

---

### Errores frecuentes

Uno de los errores más comunes consiste en pensar que la selección elimina columnas.

No es así.

La selección trabaja exclusivamente sobre las tuplas.

Otro error frecuente consiste en creer que modifica la relación original.

En realidad, siempre produce una nueva relación sin alterar la existente.

---

### Ideas clave

* La selección filtra tuplas según una condición.
* Se representa mediante la letra griega σ.
* Conserva todos los atributos de la relación original.
* Produce una nueva relación sin modificar la existente.
* Constituye la base conceptual de la cláusula `WHERE` en SQL.

