# Ejercicios guiados

## Introducción

Hasta este momento hemos estudiado los operadores fundamentales del Álgebra Relacional de forma individual.

Sin embargo, conocer la teoría no garantiza saber resolver problemas.

La única forma de desarrollar soltura consiste en practicar el razonamiento de manera sistemática.

El objetivo de este capítulo no es que el estudiante memorice expresiones algebraicas.

El objetivo es aprender **cómo pensar** antes de escribir una consulta.

Por ese motivo, todos los ejercicios seguirán siempre la misma estructura:

1. Comprender el problema.
2. Identificar las relaciones implicadas.
3. Seleccionar los operadores necesarios.
4. Establecer el orden de aplicación.
5. Obtener la relación resultado.

No nos preocuparemos todavía por la sintaxis exacta de SQL. Esa llegará en las próximas clases.

---

### Ejercicio 1

#### Enunciado

La empresa desea conocer el nombre y el precio de todos los productos cuyo precio sea superior a 500 euros.

---

#### Paso 1. ¿Qué información necesitamos?

* Nombre
* Precio

---

#### Paso 2. ¿Dónde está esa información?

Toda ella se encuentra en la relación ​**Producto**​.

No es necesario combinar varias relaciones.

---

#### Paso 3. ¿Existe algún filtro?

Sí.

Únicamente interesan los productos cuyo precio sea superior a 500 euros.

Necesitamos una ​**selección**​.

---

#### Paso 4. ¿Qué atributos deben mostrarse?

Solo:

* Nombre
* Precio

Necesitamos una ​**proyección**​.

---

#### Solución conceptual

```text
Producto
      ↓
Selección (Precio > 500)
      ↓
Proyección (Nombre, Precio)
```

---

### Ejercicio 2

#### Enunciado

Obtener el nombre de todos los clientes que viven en Santander.

---

#### Paso 1

La información procede únicamente de la relación ​**Cliente**​.

---

#### Paso 2

Debemos filtrar:

Ciudad = Santander

Aplicamos una ​**selección**​.

---

#### Paso 3

Solo interesa mostrar el nombre.

Aplicamos una ​**proyección**​.

---

#### Resultado conceptual

```mermaid
flowchart LR

A[Cliente]

A --> B[Selección Ciudad = Santander]

B --> C[Proyección Nombre]
```

---

### Ejercicio 3

#### Enunciado

Mostrar los nombres de los clientes que han realizado algún pedido.

---

#### Paso 1

Intervienen dos relaciones.

* Cliente
* Pedido

---

#### Paso 2

Es necesario relacionarlas.

Aplicamos un ​**JOIN**​.

---

#### Paso 3

Solo queremos mostrar:

Nombre

Aplicamos una proyección.

---

#### Secuencia de operaciones

```text
Cliente

JOIN

Pedido

↓

Proyección Nombre
```

---

### Ejercicio 4

#### Enunciado

Obtener todos los productos cuyo stock sea inferior a cinco unidades.

---

#### Razonamiento

No es necesario realizar un JOIN.

Toda la información pertenece a la relación ​**Producto**​.

Aplicamos únicamente una selección.

---

### Ejercicio 5

#### Enunciado

La empresa dispone de dos relaciones:

* ProductosPromocionVerano
* ProductosPromocionInvierno

Se desea obtener el catálogo completo de promociones.

---

#### Operador adecuado

La información debe reunirse en una única relación.

Necesitamos una ​**unión**​.

---

### Ejercicio 6

#### Enunciado

La empresa desea conocer los clientes registrados que todavía no han realizado ninguna compra.

---

#### Relaciones

* Cliente
* ClientesConPedidos

---

#### Operador

Queremos los clientes presentes en la primera relación pero ausentes en la segunda.

Necesitamos una ​**diferencia**​.

---

### Ejercicio 7

#### Enunciado

Mostrar únicamente las ciudades donde existen clientes registrados.

---

#### Observación importante

Varios clientes pueden vivir en la misma ciudad.

---

#### Operador

Aplicamos una proyección sobre el atributo ​**Ciudad**​.

El resultado contendrá cada ciudad una sola vez porque el Álgebra Relacional elimina automáticamente los duplicados.

---

### Cómo comprobar una solución

Antes de considerar correcta una consulta conviene responder mentalmente estas preguntas.

* ¿He identificado correctamente las relaciones implicadas?
* ¿Estoy filtrando filas o eliminando columnas?
* ¿Existe alguna unión entre varias relaciones?
* ¿Necesito eliminar duplicados?
* ¿El resultado contiene exactamente la información solicitada?

Responder afirmativamente a todas ellas suele indicar que el razonamiento es correcto.

---

### Errores frecuentes durante la resolución

Los estudiantes suelen cometer varios errores repetitivos.

El primero consiste en pensar inmediatamente en SQL.

El segundo consiste en utilizar un JOIN cuando toda la información ya se encuentra en una única relación.

También es muy habitual confundir selección y proyección.

Finalmente, muchos alumnos intentan escribir una única expresión compleja sin haber dividido antes el problema en pasos más pequeños.

---

### Ideas clave

* Resolver consultas consiste en razonar, no en memorizar sintaxis.
* Cada problema puede descomponerse en una secuencia de operadores sencillos.
* Antes de escribir una consulta conviene identificar relaciones, filtros y atributos.
* La práctica sistemática desarrolla la capacidad de análisis necesaria para SQL.
* Pensar primero en Álgebra Relacional facilita enormemente el diseño de consultas correctas.

