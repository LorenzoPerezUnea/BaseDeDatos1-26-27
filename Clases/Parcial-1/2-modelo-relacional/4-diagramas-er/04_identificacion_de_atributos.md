# Identificación de atributos

Después de descubrir las entidades debemos preguntarnos qué información necesita almacenar la empresa sobre cada una de ellas.

La respuesta a esta pregunta nos permitirá identificar los ​**atributos**​.

Los atributos describen las características de una entidad.

Mientras que una entidad representa un objeto del negocio, un atributo representa una propiedad de ese objeto.

### Empezar por lo imprescindible

Un error frecuente consiste en intentar registrar toda la información imaginable desde el primer momento.

En realidad, durante el análisis inicial conviene identificar únicamente los datos necesarios para que el negocio funcione.

Los atributos adicionales podrán incorporarse más adelante si aparecen nuevas necesidades.

### Ejemplo sencillo

Consideremos la entidad ​**Cliente**​.

Durante las entrevistas obtenemos la siguiente información.

La empresa necesita conocer:

* Nombre.
* Apellidos.
* Teléfono.
* Correo electrónico.
* Fecha de alta.

El resultado será:

```text
Cliente

IdCliente
Nombre
Apellidos
Telefono
Correo
FechaAlta
```

Cada atributo aporta información relevante sobre el cliente.

### Cómo descubrir atributos

Una buena estrategia consiste en preguntar:

> ¿Qué información necesita conocer la empresa sobre este objeto?

Por ejemplo, para un producto podrían aparecer respuestas como:

* Nombre.
* Precio.
* Stock.
* Marca.
* Peso.
* Descripción.

No todos estos datos serán obligatorios.

Dependerá de las necesidades reales del negocio.

### Distinguir atributos de relaciones

A veces resulta difícil decidir si un dato debe representarse como atributo o como relación.

Por ejemplo:

**Categoría del producto**

Existen dos posibilidades.

Si las categorías son un conjunto fijo de textos:

```text
Categoria = "Portátiles"
```

podría bastar con un atributo.

Sin embargo, si cada categoría posee información propia, será preferible crear una entidad independiente.

En nuestra empresa comercial utilizaremos esta segunda opción.

### Evitar atributos calculables

Otro principio importante consiste en no almacenar datos que puedan calcularse fácilmente.

Por ejemplo:

```text
Edad
```

La edad cambia continuamente.

Es preferible almacenar:

```text
FechaNacimiento
```

y calcular la edad cuando sea necesaria.

De esta forma evitamos inconsistencias.

### Pensar en el futuro

Durante el análisis debemos preguntarnos si un atributo podría cambiar con el tiempo.

Por ejemplo:

* Teléfono.
* Correo electrónico.
* Dirección.

Estos datos cambian con frecuencia.

Por el contrario, un identificador interno normalmente permanecerá constante.

Esta diferencia será importante cuando estudiemos las claves primarias.

### Caso práctico

Nuestro modelo comienza a adquirir mayor detalle.

```text
Cliente

IdCliente
Nombre
Apellidos
Telefono
Correo

Producto

IdProducto
Nombre
Precio
Stock

Pedido

IdPedido
Fecha
Estado
```

Todavía es un modelo sencillo, pero ya contiene suficiente información para representar correctamente la actividad principal de la empresa.

### Ideas clave

* Los atributos describen las propiedades de una entidad.
* Deben responder a necesidades reales del negocio.
* Conviene evitar datos calculables.
* No toda la información debe incorporarse desde el principio.
* Un buen conjunto de atributos facilita el diseño posterior del modelo relacional.

