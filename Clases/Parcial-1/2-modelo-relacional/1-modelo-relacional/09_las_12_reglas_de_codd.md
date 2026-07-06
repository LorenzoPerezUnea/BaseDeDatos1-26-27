# Las doce reglas de Codd

Cuando Edgar F. Codd propuso el Modelo Relacional en 1970, muchas empresas comenzaron a comercializar productos que afirmaban ser "bases de datos relacionales". Sin embargo, cada fabricante interpretaba el término de una manera diferente.

Algunos sistemas utilizaban tablas, pero seguían obligando al programador a conocer cómo estaban almacenados físicamente los datos. Otros incorporaban algunas ideas del Modelo Relacional, pero ignoraban principios fundamentales.

Para evitar esta situación, Codd publicó en 1985 un conjunto de criterios conocidos como **las doce reglas de Codd** (en realidad son trece, ya que la numeración comienza en la regla 0).

Estas reglas no fueron concebidas como una lista para memorizar, sino como una forma de evaluar hasta qué punto un Sistema Gestor de Bases de Datos podía considerarse realmente relacional.

### Regla 0. Regla fundamental

> Un sistema solo puede considerarse relacional si administra la base de datos exclusivamente mediante sus capacidades relacionales.

Esta regla resume todas las demás.

No basta con almacenar datos en tablas. Todas las operaciones importantes deben realizarse respetando el Modelo Relacional.

### Regla 1. Regla de la información

Toda la información debe representarse únicamente mediante valores almacenados en tablas.

No deben existir mecanismos ocultos para almacenar parte de la información fuera de las relaciones.

Esta idea convierte a las tablas en el elemento central del modelo.

### Regla 2. Acceso garantizado

Todo dato debe ser accesible utilizando:

* El nombre de la tabla.
* El valor de la clave primaria.
* El nombre del atributo.

No debería ser necesario conocer dónde se encuentra almacenado físicamente el dato.

Esta regla proporciona independencia respecto al almacenamiento interno.

### Regla 3. Tratamiento sistemático de valores nulos

Los valores nulos representan la ausencia de información.

El sistema debe tratarlos de forma coherente y diferenciarlos claramente de:

* El valor cero.
* Una cadena vacía.
* Un valor desconocido.

Más adelante veremos que el tratamiento de los valores `NULL` constituye uno de los aspectos más particulares del lenguaje SQL.

### Regla 4. Catálogo dinámico

La propia descripción de la base de datos debe almacenarse también como información relacional.

Esto permite consultar metadatos utilizando el mismo lenguaje empleado para consultar los datos.

Por ejemplo, un administrador puede obtener información sobre tablas, columnas o restricciones mediante consultas al catálogo del sistema.

### Regla 5. Lenguaje de datos completo

El sistema debe disponer de un lenguaje capaz de realizar todas las operaciones necesarias.

Entre ellas:

* Definir estructuras.
* Consultar datos.
* Modificar información.
* Gestionar permisos.
* Administrar transacciones.

SQL nació precisamente para cubrir estas necesidades.

### Regla 6. Actualización de vistas

Siempre que sea posible, una vista actualizable debería poder modificarse igual que una tabla.

Aunque en la práctica esta regla presenta numerosas limitaciones, la mayoría de los SGBD modernos permiten actualizar determinadas vistas sencillas.

### Regla 7. Inserción, actualización y borrado de alto nivel

El sistema debe permitir operar sobre conjuntos completos de registros, no únicamente sobre registros individuales.

Esta es una de las mayores diferencias entre SQL y muchos lenguajes de programación.

Por ejemplo:

```sql
UPDATE productos
SET precio = precio * 1.05;
```

Esta única instrucción puede modificar miles de registros simultáneamente.

### Regla 8. Independencia física

Los programas no deberían verse afectados si cambia la organización física de los datos.

Por ejemplo:

* Crear un índice.
* Cambiar el tipo de almacenamiento.
* Reorganizar archivos internos.

Todas estas modificaciones deberían ser transparentes para las aplicaciones.

### Regla 9. Independencia lógica

Las aplicaciones deberían seguir funcionando incluso cuando cambie parcialmente la estructura lógica de la base de datos.

Aunque en la práctica esta independencia nunca es absoluta, sigue siendo uno de los objetivos fundamentales del diseño relacional.

### Regla 10. Independencia de integridad

Las restricciones de integridad deben definirse dentro del propio sistema gestor y no repartirse entre las aplicaciones.

Esto garantiza que todos los programas respeten exactamente las mismas reglas.

### Regla 11. Independencia de distribución

El usuario no debería notar diferencias entre trabajar con una base de datos centralizada o distribuida en varios servidores.

Hoy en día esta regla tiene especial importancia en servicios en la nube y arquitecturas distribuidas.

### Regla 12. No subversión

Si el sistema ofrece mecanismos de bajo nivel para acceder a los datos, dichos mecanismos no deben permitir incumplir las reglas del Modelo Relacional.

En otras palabras, ninguna herramienta debe poder "saltarse" las restricciones establecidas por el sistema.

### ¿Es necesario memorizar las reglas?

No.

Lo importante es comprender la filosofía que hay detrás de ellas.

Todas persiguen un mismo objetivo:

* Mantener la consistencia de la información.
* Facilitar el desarrollo de aplicaciones.
* Independizar los programas de la forma en que se almacenan los datos.

Más adelante veremos que muchos conceptos actuales de SQL proceden directamente de estas reglas.

### Ideas clave

* Las reglas de Codd establecen los principios que debe cumplir un sistema relacional.
* Su objetivo es evaluar la fidelidad de un SGBD al Modelo Relacional.
* Muchas características de SQL derivan directamente de estas reglas.
* Ningún SGBD comercial cumple todas las reglas de forma absoluta, pero constituyen la referencia teórica del modelo.

