# Preparación para la normalización

Con esta clase hemos estudiado el fundamento teórico del diseño relacional.

Ahora estamos preparados para abordar uno de los temas más importantes de toda la asignatura:

> **La normalización.**

Aunque muchos estudiantes consideran la normalización como un conjunto de reglas que deben memorizarse, en realidad es una consecuencia directa de las dependencias funcionales.

Comprender esta idea facilitará enormemente las próximas clases.

### ¿Qué es normalizar?

Normalizar consiste en reorganizar las tablas de una base de datos para reducir redundancias y evitar anomalías de inserción, actualización y eliminación.

No se trata de crear más tablas por crear.

El objetivo es que cada dato se almacene en el lugar donde realmente pertenece.

### El papel de las dependencias

Las dependencias funcionales nos indican qué atributos dependen de otros.

Gracias a ellas podemos detectar problemas como:

* información repetida;
* dependencias parciales;
* dependencias transitivas;
* claves mal definidas.

La normalización utilizará precisamente estas situaciones para decidir cuándo dividir una tabla.

### Un ejemplo sencillo

Supongamos la siguiente tabla.

```text
PRODUCTO

IdProducto
NombreProducto
Precio
IdCategoria
NombreCategoria
```

Sabemos que:

```text
IdCategoria
→
NombreCategoria
```

Esto significa que el nombre de la categoría no depende realmente del producto.

La normalización propondrá crear una nueva tabla.

```text
CATEGORIA

IdCategoria
NombreCategoria
```

De esta forma eliminamos información duplicada.

### Lo que veremos en las próximas clases

En la siguiente parte del curso estudiaremos, paso a paso:

* Primera Forma Normal (1FN).
* Segunda Forma Normal (2FN).
* Tercera Forma Normal (3FN).
* Forma Normal de Boyce-Codd (BCNF).
* Introducción a Cuarta y Quinta Forma Normal.

Cada una resolverá un tipo concreto de problema detectado mediante dependencias funcionales.

### Nuestro caso práctico

La empresa comercial que hemos utilizado desde el inicio del curso continuará evolucionando.

Partiremos del modelo relacional construido en las clases anteriores y lo refinaremos progresivamente hasta obtener un diseño completamente normalizado y preparado para implementarse en MySQL.

Esto permitirá observar cómo la teoría se aplica directamente a un caso real.

### Ideas clave

* La normalización se basa en las dependencias funcionales.
* Su objetivo es reducir redundancias y mejorar la integridad de los datos.
* Cada Forma Normal resuelve un problema diferente.
* Las dependencias estudiadas en esta clase serán la herramienta principal para normalizar.
* El caso práctico seguirá evolucionando durante las próximas sesiones.

