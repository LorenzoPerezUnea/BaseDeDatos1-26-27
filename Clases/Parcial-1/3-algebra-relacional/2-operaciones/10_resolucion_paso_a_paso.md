# Resolución paso a paso

## Introducción

Después de estudiar los operadores fundamentales del Álgebra Relacional, el siguiente paso consiste en aprender a utilizarlos para resolver problemas reales.

Cuando un estudiante comienza a trabajar con consultas suele intentar escribir directamente la expresión completa.

Sin embargo, esa estrategia rara vez funciona.

Las consultas complejas no se construyen de una sola vez.

Se construyen resolviendo pequeños problemas consecutivos.

Esta forma de razonar resulta muy similar a la utilizada en programación cuando se divide un problema grande en funciones más pequeñas.

En Álgebra Relacional haremos exactamente lo mismo.

Aprenderemos a descomponer una consulta en una secuencia de operaciones simples.

---

### Un método sistemático

A lo largo del resto del curso utilizaremos siempre la misma metodología.

Antes de pensar en símbolos algebraicos o en SQL responderemos las siguientes preguntas:

1. ¿Qué información solicita el usuario?
2. ¿En qué relaciones se encuentra esa información?
3. ¿Qué relaciones deben combinarse?
4. ¿Qué filtros deben aplicarse?
5. ¿Qué atributos deben aparecer en el resultado?
6. ¿Cuál es el orden lógico de las operaciones?

Este procedimiento evita muchos errores y facilita enormemente el diseño de consultas.

---

### Problema 1

La dirección comercial solicita:

> "Mostrar el nombre y el precio de todos los productos cuyo stock sea inferior a diez unidades."

#### Paso 1. Localizar la información

Toda la información se encuentra en la relación ​**Producto**​.

No es necesario combinar varias relaciones.

#### Paso 2. Identificar el filtro

Solo interesan los productos con:

```text
Stock < 10
```

Esto implica una ​**selección**​.

#### Paso 3. Identificar la información necesaria

El informe únicamente necesita:

* Nombre
* Precio

Esto implica una ​**proyección**​.

#### Paso 4. Orden lógico

El razonamiento completo es:

```mermaid
flowchart LR

A[Producto]

A --> B[Selección]

B --> C[Productos con Stock < 10]

C --> D[Proyección]

D --> E[Nombre y Precio]
```

Obsérvese que todavía no hemos escrito ninguna consulta SQL.

Y, sin embargo, el procedimiento ya está completamente definido.

---

### Problema 2

Ahora la empresa desea conocer:

> "El nombre de los clientes que realizaron pedidos durante el mes de marzo."

#### Paso 1

La información aparece repartida entre:

* Cliente
* Pedido

#### Paso 2

Es necesario relacionarlas.

Esto implica un ​**JOIN**​.

#### Paso 3

Solo interesan los pedidos de marzo.

Necesitamos una ​**selección**​.

#### Paso 4

Finalmente solo queremos mostrar:

* Nombre

Aplicaremos una ​**proyección**​.

---

### El orden correcto

Muchos estudiantes plantean inmediatamente un JOIN completo.

Sin embargo, desde el punto de vista del razonamiento suele resultar más eficiente pensar así:

1. Seleccionar únicamente los pedidos de marzo.
2. Relacionarlos con los clientes.
3. Mostrar únicamente el nombre.

Reducir cuanto antes el volumen de información simplifica el resto de operaciones.

Más adelante veremos que los optimizadores intentan precisamente reorganizar las consultas siguiendo este principio.

---

### Problema 3

La dirección desea conocer:

> "Los nombres de los productos vendidos durante el último trimestre."

La información aparece distribuida entre varias relaciones.

* Producto
* LineaPedido
* Pedido

Podemos razonar de la siguiente manera.

1. Seleccionar los pedidos del último trimestre.
2. Relacionarlos con sus líneas.
3. Relacionar esas líneas con los productos.
4. Mostrar únicamente el nombre del producto.

Aunque el resultado final parezca complejo, observamos que únicamente estamos combinando operadores que ya conocemos.

---

### Un procedimiento reutilizable

Uno de los objetivos más importantes del curso consiste en desarrollar un hábito de trabajo.

Cada vez que recibas un nuevo problema intenta evitar la tentación de escribir SQL inmediatamente.

En su lugar:

* identifica las relaciones;
* identifica los filtros;
* identifica las uniones;
* identifica la información que debe mostrarse.

Solo cuando el razonamiento esté claro merece la pena escribir la consulta.

Este procedimiento funciona igual de bien para consultas sencillas que para consultas con decenas de tablas.

---

### Relación con la optimización

Los sistemas gestores modernos siguen una filosofía muy parecida.

Cuando reciben una consulta SQL no la ejecutan directamente.

Primero la transforman en una secuencia de operadores algebraicos.

Después buscan un orden más eficiente para esas operaciones.

Por tanto, aprender este método de resolución también ayuda a comprender el funcionamiento interno del optimizador.

---

### Errores frecuentes

Un error muy común consiste en intentar construir la consulta completa sin haber identificado previamente qué operadores son necesarios.

También es frecuente comenzar uniendo todas las tablas disponibles y aplicar los filtros al final.

En muchas ocasiones resulta más eficiente filtrar cuanto antes para reducir el número de tuplas que deberán procesarse posteriormente.

---

### Ideas clave

* Las consultas complejas deben resolverse paso a paso.
* Antes de escribir una consulta conviene identificar relaciones, filtros y atributos.
* La descomposición del problema facilita enormemente el razonamiento.
* El orden de las operaciones influye en la eficiencia.
* Esta metodología será utilizada durante todo el resto del curso.

