# Caso práctico de la empresa

## Introducción

A lo largo de esta asignatura hemos utilizado siempre el mismo caso de estudio: una empresa dedicada a la comercialización de productos tecnológicos mediante tiendas físicas y comercio electrónico.

Mantener un único caso práctico durante todo el curso tiene una ventaja fundamental.

El estudiante deja de invertir esfuerzo en comprender nuevos escenarios y puede concentrarse en aprender los conceptos propios de las bases de datos.

En este capítulo reuniremos todos los operadores estudiados en una situación lo más cercana posible al trabajo diario de una empresa real.

---

### Situación inicial

La dirección solicita un informe comercial con los siguientes requisitos:

1. Mostrar únicamente los pedidos realizados durante el último mes.
2. Asociar cada pedido con el cliente correspondiente.
3. Mostrar el nombre del cliente.
4. Mostrar el producto vendido.
5. Mostrar la cantidad adquirida.
6. Mostrar el precio de venta registrado en el pedido.

La información necesaria no se encuentra en una única relación.

Está distribuida entre varias tablas del modelo.

---

### Relaciones implicadas

Para resolver el problema intervienen las siguientes relaciones.

* Cliente
* Pedido
* LineaPedido
* Producto

Cada una almacena únicamente una parte de la información.

| Relación   | Información principal  |
| ------------- | ------------------------- |
| Cliente     | Datos del cliente       |
| Pedido      | Cabecera del pedido     |
| LineaPedido | Productos vendidos      |
| Producto    | Catálogo de artículos |

---

### Estrategia de resolución

Podemos dividir el problema en varias etapas.

#### Primera etapa

Seleccionar únicamente los pedidos correspondientes al último mes.

Con ello reducimos considerablemente el volumen de información.

---

#### Segunda etapa

Relacionar esos pedidos con los clientes.

Ahora conocemos quién realizó cada compra.

---

#### Tercera etapa

Relacionar los pedidos con sus líneas.

Aparecen los productos concretos vendidos en cada operación.

---

#### Cuarta etapa

Relacionar las líneas con la relación ​**Producto**​.

Ahora podemos obtener el nombre comercial de cada artículo.

---

#### Quinta etapa

Realizar una proyección para conservar únicamente los atributos necesarios para el informe.

---

### Flujo completo

```mermaid
flowchart LR

A[Pedido]

A --> B[Selección Último mes]

B --> C[JOIN Cliente]

C --> D[JOIN LineaPedido]

D --> E[JOIN Producto]

E --> F[Proyección Informe Final]
```

Este diagrama resume el razonamiento seguido por el sistema.

Obsérvese que el problema aparentemente complejo termina resolviéndose mediante una secuencia de operaciones muy sencillas.

---

### ¿Qué hemos utilizado?

En esta consulta aparecen prácticamente todos los conceptos estudiados hasta ahora.

* Selección.
* JOIN.
* Proyección.
* Composición de operadores.

No ha sido necesario introducir ningún concepto nuevo.

Simplemente hemos combinado adecuadamente los operadores ya conocidos.

---

### Preparando el salto a SQL

Si observamos cuidadosamente el flujo anterior, comprobaremos que prácticamente coincide con la estructura de una consulta SQL típica.

En las próximas clases aprenderemos a escribir esa misma consulta utilizando la sintaxis del lenguaje SQL.

La diferencia será únicamente la forma de escribirla.

El razonamiento seguirá siendo exactamente el mismo.

---

### Reflexión final

Uno de los mayores errores al aprender SQL consiste en pensar que cada consulta es un problema completamente nuevo.

En realidad, la mayoría de las consultas profesionales siguen siempre un patrón muy parecido.

1. Seleccionar los datos relevantes.
2. Relacionar las tablas necesarias.
3. Elegir los atributos que aparecerán en el resultado.

Cambian las tablas y cambian las condiciones, pero el proceso mental permanece prácticamente inalterado.

Comprender este patrón constituye uno de los aprendizajes más valiosos de esta asignatura.

---

### Ideas clave

* Los problemas reales suelen requerir varias relaciones simultáneamente.
* Los operadores del Álgebra Relacional pueden combinarse para resolver consultas complejas.
* El razonamiento siempre debe preceder a la escritura de SQL.
* Un buen análisis reduce la complejidad aparente de cualquier consulta.
* El mismo proceso será reutilizado durante todo el bloque dedicado al lenguaje SQL.

