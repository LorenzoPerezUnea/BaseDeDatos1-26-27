# Composición de operaciones

## Introducción

Uno de los aspectos más elegantes del Álgebra Relacional es que todos sus operadores comparten una propiedad fundamental.

**Siempre producen una nueva relación.**

A primera vista puede parecer un detalle sin demasiada importancia.

Sin embargo, esta característica convierte al Álgebra Relacional en un sistema extraordinariamente flexible.

Si cada operador produce otra relación, esa nueva relación puede convertirse inmediatamente en la entrada del siguiente operador.

Gracias a esta idea es posible construir consultas muy complejas utilizando únicamente un pequeño conjunto de operaciones sencillas.

Esta propiedad recibe el nombre de **cierre** y constituye uno de los pilares del modelo relacional.

---

### Una analogía sencilla

Imaginemos una fábrica.

Cada máquina recibe una pieza.

Realiza una transformación.

Entrega otra pieza.

La siguiente máquina trabaja sobre esa nueva pieza.

Y así sucesivamente.

El resultado final depende de toda la cadena de transformaciones.

Las consultas algebraicas funcionan exactamente igual.

Cada operador recibe una relación.

La transforma.

Entrega otra relación.

El siguiente operador continúa el proceso.

---

### Un ejemplo paso a paso

Supongamos que la dirección comercial solicita:

> "Mostrar el nombre y el precio de los productos cuyo stock sea inferior a diez unidades."

Podemos descomponer el problema.

**Paso 1**

Partimos de la relación:

**Producto**

---

**Paso 2**

Aplicamos una selección.

Conservamos únicamente los productos cuyo stock sea menor que diez.

---

**Paso 3**

Sobre esa nueva relación aplicamos una proyección.

Conservamos únicamente:

* Nombre
* Precio

El resultado final responde exactamente a la petición inicial.

Cada operador trabaja exclusivamente sobre el resultado producido por el anterior.

---

### Visualización

```mermaid
flowchart LR

A[Producto]

A --> B[Selección]

B --> C[Productos con poco stock]

C --> D[Proyección]

D --> E[Nombre y Precio]
```

La consulta completa aparece representada como una cadena de transformaciones sucesivas.

---

### Un ejemplo más complejo

Supongamos ahora la siguiente petición.

> "Obtener el nombre de los clientes que realizaron pedidos durante este mes."

Podemos razonar del siguiente modo.

1. Partimos de Pedido.
2. Seleccionamos únicamente los pedidos del mes actual.
3. Relacionamos esos pedidos con Cliente.
4. Proyectamos únicamente el nombre.

Aunque el resultado sea una consulta aparentemente sencilla, internamente ya estamos utilizando varios operadores encadenados.

Esta forma de pensar será exactamente la que adoptaremos cuando estudiemos consultas SQL de varias tablas.

---

### La importancia del orden

En muchas ocasiones el orden en que se aplican las operaciones modifica el trabajo que debe realizar el sistema.

Supongamos dos estrategias.

**Estrategia A**

* producto cartesiano;
* selección;
* proyección.

**Estrategia B**

* proyección;
* selección;
* producto cartesiano.

No siempre producirán el mismo resultado ni tendrán el mismo coste.

Precisamente una de las tareas principales del optimizador consiste en reorganizar estas operaciones para ejecutar la consulta de la forma más eficiente posible.

Por ello resulta tan importante comprender la composición de operadores antes de estudiar optimización.

---

### Aplicación al caso de estudio

Nuestra empresa genera diariamente numerosos informes.

Cada informe puede requerir varias operaciones consecutivas.

Por ejemplo:

* seleccionar únicamente los pedidos del último trimestre;
* relacionarlos con sus clientes;
* obtener únicamente determinados atributos;
* ordenar posteriormente la información.

Aunque el usuario perciba una única consulta, internamente el sistema ejecuta una secuencia de operadores muy similar a la que acabamos de estudiar.

---

### Relación con SQL

Cuando escribimos una consulta SQL compleja solemos verla como una única instrucción.

Sin embargo, el optimizador la transforma en un árbol de operaciones algebraicas.

Ese árbol representa precisamente la composición de operadores que acabamos de estudiar.

Más adelante aprenderemos a interpretar esos árboles mediante los planes de ejecución.

---

### Errores frecuentes

Muchos estudiantes intentan comprender consultas complejas leyéndolas de izquierda a derecha como si fueran un texto.

Resulta mucho más útil descomponerlas en una secuencia de pequeñas operaciones.

También es frecuente olvidar que cada operador recibe como entrada el resultado del anterior, no necesariamente una tabla almacenada en la base de datos.

---

### Ideas clave

* Todos los operadores producen nuevas relaciones.
* Esta propiedad permite encadenar operaciones indefinidamente.
* Las consultas complejas pueden descomponerse en una secuencia de transformaciones sencillas.
* El orden de las operaciones influye en el trabajo realizado por el sistema.
* La composición de operadores constituye la base de los planes de ejecución utilizados por los SGBD.

