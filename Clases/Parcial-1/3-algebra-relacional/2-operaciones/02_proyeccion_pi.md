# Proyección (π)

## Introducción

Si la **selección** responde a la pregunta ​*"¿Qué filas necesito?"*​, la **proyección** responde a una pregunta completamente distinta:

> **¿Qué información necesito de cada fila?**

En muchas ocasiones no resulta necesario trabajar con todos los atributos de una relación.

Por ejemplo, el departamento de marketing puede necesitar únicamente el nombre y el correo electrónico de los clientes para preparar una campaña.

El departamento financiero quizá solo requiera el identificador del pedido y su importe.

El responsable de almacén podría querer una lista formada únicamente por el nombre del producto y las unidades disponibles.

En ninguno de estos casos deseamos eliminar clientes, pedidos o productos.

Lo único que queremos es ​**descartar la información que no resulta relevante**​.

Ese es precisamente el objetivo de la proyección.

---

### La intuición

Imaginemos que tenemos delante la ficha completa de un cliente.

Contiene mucha información:

* identificador;
* nombre;
* apellidos;
* dirección;
* ciudad;
* código postal;
* teléfono;
* correo electrónico;
* fecha de registro.

Ahora imaginemos que únicamente necesitamos enviar un boletín informativo.

Toda esa información adicional deja de ser necesaria.

Podemos construir una nueva ficha que conserve únicamente:

* Nombre
* Correo electrónico

No estamos eliminando clientes.

Simplemente estamos eliminando atributos.

Ese es exactamente el comportamiento de la proyección.

---

### Definición formal

La proyección se representa mediante la letra griega ​**pi (π)**​.

Su forma general es:

```text
π atributo1, atributo2, ... (Relación)
```

Donde:

* **π** representa el operador de proyección.
* la lista de atributos indica qué columnas deben conservarse;
* la relación constituye el conjunto de datos de entrada.

El resultado es siempre una nueva relación formada únicamente por los atributos seleccionados.

---

### ¿Qué cambia y qué permanece?

A diferencia de la selección, la proyección ​**modifica la estructura de la relación**​.

Las tuplas continúan representando los mismos elementos, pero ahora contienen menos información.

Podemos resumirlo así:

| Elemento                              | ¿Cambia?       |
| --------------------------------------- | ----------------- |
| Número de atributos                  | Sí             |
| Nombre de los atributos               | Puede reducirse |
| Dominios de los atributos conservados | No              |
| Número de tuplas                     | Normalmente no  |

Es importante observar la palabra ​**normalmente**​.

Existe una particularidad que estudiaremos a continuación.

---

### La eliminación de duplicados

Recordemos que una relación es un conjunto.

Y un conjunto no puede contener elementos repetidos.

Esto significa que, después de realizar una proyección, pueden aparecer tuplas idénticas.

Cuando esto ocurre, el Álgebra Relacional conserva únicamente una de ellas.

Veamos un ejemplo.

Relación ​**Cliente**​:

| IdCliente | Nombre       | Ciudad    |
| ----------: | -------------- | ----------- |
|         1 | Ana Ruiz     | Santander |
|         2 | Luis Pérez  | Bilbao    |
|         3 | Marta Gómez | Santander |
|         4 | Pedro López | Bilbao    |

Si proyectamos únicamente el atributo ​**Ciudad**​, obtenemos inicialmente:

| Ciudad    |
| ----------- |
| Santander |
| Bilbao    |
| Santander |
| Bilbao    |

Sin embargo, esa relación contiene duplicados.

El resultado correcto será:

| Ciudad    |
| ----------- |
| Santander |
| Bilbao    |

Esta característica diferencia claramente al Álgebra Relacional de SQL, donde los duplicados solo desaparecen cuando se utiliza `DISTINCT`.

---

### Aplicación al caso de estudio

Supongamos que el departamento comercial necesita elaborar un listado telefónico.

De la relación **Cliente** únicamente interesan:

* Nombre
* Telefono

Todos los demás atributos resultan irrelevantes para esa tarea.

La proyección genera una nueva relación mucho más pequeña y sencilla de manejar.

Esta reducción de información también disminuye el volumen de datos que debe procesar el sistema.

---

### Proyección y eficiencia

Aunque el objetivo principal de la proyección es obtener únicamente la información necesaria, también aporta ventajas desde el punto de vista del rendimiento.

Cuantos menos atributos deban transportarse entre el servidor y la aplicación:

* menor cantidad de memoria será necesaria;
* menor volumen de datos viajará por la red;
* más sencilla será la presentación de los resultados.

Por esta razón constituye una buena práctica solicitar únicamente las columnas realmente necesarias.

Esta recomendación aparecerá de nuevo cuando estudiemos SQL.

---

### Diferencias con la selección

La selección y la proyección suelen confundirse durante las primeras semanas.

La siguiente tabla resume sus diferencias principales.

| Selección                   | Proyección                     |
| ------------------------------ | --------------------------------- |
| Trabaja sobre las tuplas     | Trabaja sobre los atributos     |
| Filtra filas                 | Elimina columnas                |
| Mantiene la estructura       | Modifica la estructura          |
| Conserva todos los atributos | Conserva solo algunos atributos |

Recordar esta comparación suele evitar muchos errores.

---

### Relación con SQL

Más adelante veremos que la lista de columnas situada inmediatamente después de la palabra `SELECT` constituye precisamente una proyección.

Cuando escribimos:

```sql
SELECT Nombre, Telefono
FROM Cliente;
```

Estamos indicando exactamente qué atributos deseamos conservar en el resultado.

La correspondencia con el operador π es prácticamente directa.

---

### Errores frecuentes

El error más habitual consiste en pensar que la proyección elimina determinadas filas.

No es así.

La proyección modifica únicamente los atributos visibles.

También es frecuente olvidar que, desde el punto de vista del Álgebra Relacional, las tuplas duplicadas desaparecen automáticamente tras la proyección.

Esta propiedad será una de las principales diferencias respecto a SQL.

---

### Ideas clave

* La proyección selecciona atributos, no tuplas.
* Se representa mediante la letra griega π.
* Modifica la estructura de la relación conservando únicamente las columnas necesarias.
* En Álgebra Relacional elimina automáticamente los duplicados resultantes.
* Constituye la base conceptual de la lista de columnas utilizada en `SELECT`.

