# Ejemplos intuitivos

## Introducción

Después de estudiar los conceptos fundamentales del Álgebra Relacional puede surgir una sensación común entre muchos estudiantes: la teoría parece clara, pero todavía cuesta imaginar cómo se utiliza para resolver problemas reales.

Esta impresión es completamente normal.

Los símbolos matemáticos y las definiciones formales resultan mucho más fáciles de comprender cuando se aplican sobre situaciones conocidas.

En este capítulo construiremos varios ejemplos utilizando la base de datos de nuestra empresa de venta de productos tecnológicos. El objetivo no es aprender todavía todos los operadores en profundidad, sino desarrollar la intuición necesaria para entender cómo razona una consulta algebraica.

### Ejemplo 1. Buscar clientes de una ciudad

Supongamos que el departamento comercial desea contactar únicamente con los clientes residentes en Santander.

Visualmente podríamos imaginar la relación **Cliente** de la siguiente forma:

| IdCliente | Nombre       | Ciudad    |
| ----------: | -------------- | ----------- |
|         1 | Ana Ruiz     | Santander |
|         2 | Luis Pérez  | Bilbao    |
|         3 | Marta Gómez | Santander |
|         4 | Carlos Díaz | Oviedo    |

Nuestro objetivo consiste en conservar únicamente aquellas tuplas cuya ciudad sea Santander.

Conceptualmente, el proceso puede representarse así:

```mermaid
flowchart LR

A[Relación Cliente]
-->B[Selección<br/>Ciudad = Santander]
-->C[Nueva relación]
```

El resultado sería una nueva relación formada únicamente por Ana Ruiz y Marta Gómez.

Obsérvese que la relación original no desaparece ni se modifica.

Simplemente obtenemos otra relación derivada de ella.

### Ejemplo 2. Mostrar únicamente algunos datos

Imaginemos ahora que el departamento de marketing necesita elaborar una campaña de correo electrónico.

No necesita conocer la ciudad ni el identificador del cliente.

Únicamente requiere el nombre y la dirección de correo electrónico.

En este caso no interesa eliminar filas.

Lo que se desea es eliminar columnas.

Conceptualmente el proceso sería:

```mermaid
flowchart LR

A[Cliente]
-->B[Proyección<br/>Nombre, CorreoElectronico]
-->C[Nueva relación]
```

El número de tuplas permanece igual, pero la estructura de la relación cambia porque únicamente conserva determinados atributos.

### Ejemplo 3. Dos operaciones consecutivas

Las consultas más interesantes suelen combinar varios operadores.

Supongamos ahora que queremos obtener el nombre y el correo electrónico de los clientes residentes en Santander.

El razonamiento sería:

1. Partimos de Cliente.
2. Filtramos únicamente los clientes de Santander.
3. Conservamos solo Nombre y CorreoElectronico.

Visualmente:

```mermaid
flowchart LR

A[Cliente]
-->B[Selección]
-->C[Clientes de Santander]
-->D[Proyección]
-->E[Nombre y Correo]
```

Aunque el resultado parezca sencillo, internamente ya estamos combinando varios operadores algebraicos.

Esta idea será fundamental cuando estudiemos consultas SQL complejas.

### Ejemplo 4. Productos con poco stock

Veamos un ejemplo relacionado con la gestión del almacén.

La relación **Producto** contiene, entre otros, los siguientes atributos:

* IdProducto
* Nombre
* Precio
* Stock

El responsable del almacén desea conocer únicamente aquellos productos cuyo stock sea inferior a diez unidades.

De nuevo, el razonamiento consiste simplemente en aplicar una selección.

No estamos modificando el inventario.

No estamos eliminando productos.

Únicamente estamos obteniendo una nueva relación que contiene los artículos que requieren reposición.

### Lo importante no es la sintaxis

En todos estos ejemplos hemos evitado deliberadamente escribir expresiones algebraicas completas.

¿Por qué?

Porque el objetivo de este capítulo es aprender a pensar antes de escribir.

Muchos estudiantes intentan memorizar símbolos demasiado pronto y terminan perdiendo de vista la lógica de las consultas.

Primero debemos ser capaces de responder preguntas como:

* ¿Qué información necesito?
* ¿Debo eliminar filas o columnas?
* ¿Estoy utilizando una o varias relaciones?
* ¿Qué operación representa mejor el problema?

Una vez dominado ese razonamiento, la notación y posteriormente SQL resultan mucho más sencillos.

### Errores frecuentes

Es muy habitual confundir una selección con una proyección.

La selección modifica el conjunto de tuplas conservando todos los atributos.

La proyección conserva las tuplas pero reduce el número de atributos visibles.

Distinguir claramente ambas operaciones evitará muchos errores cuando comencemos a escribir consultas más complejas.

### Ideas clave

* El Álgebra Relacional describe transformaciones sucesivas sobre relaciones.
* Cada operador resuelve un problema concreto.
* Las operaciones pueden combinarse para formar consultas más elaboradas.
* Antes de aprender la sintaxis es importante comprender el razonamiento que hay detrás de cada consulta.
* Pensar de forma algebraica facilitará enormemente el aprendizaje posterior de SQL.

