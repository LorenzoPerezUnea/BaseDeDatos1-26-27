# Primera Forma Normal

La **Primera Forma Normal (1FN)** es el primer paso del proceso de normalización y constituye la base sobre la que se apoyan todas las formas normales posteriores.

Aunque su definición formal es relativamente sencilla, sus implicaciones son muy importantes.

Antes de estudiar la regla, conviene comprender el problema que intenta resolver.

### ¿Por qué surge la Primera Forma Normal?

Imaginemos que una empresa almacena los teléfonos de sus clientes de la siguiente forma.

| IdCliente | Nombre | Teléfonos           |
| ----------: | -------- | ---------------------- |
|         1 | Ana    | 612345678, 698765432 |
|         2 | Luis   | 611111111            |

A primera vista parece una solución práctica.

Sin embargo, el atributo **Teléfonos** contiene varios valores.

Esto dificulta enormemente las consultas, las actualizaciones y la validación de los datos.

### Definición

Una relación está en **Primera Forma Normal** cuando ​**cada atributo contiene un único valor atómico para cada fila**​.

La palabra **atómico** significa que el valor no puede dividirse en otros valores desde el punto de vista del modelo de datos.

En otras palabras:

> Una celda debe contener un único dato.

### Valores atómicos

Los siguientes ejemplos cumplen la Primera Forma Normal.

| IdProducto | Nombre  | Precio |
| ------------ | --------- | -------: |
| 101        | Ratón  |  18.90 |
| 102        | Monitor | 189.00 |

Cada celda contiene un único valor.

En cambio, esta tabla no cumple la 1FN.

| Cliente | Correos                                                                   |
| --------- | --------------------------------------------------------------------------- |
| Ana     | [ana@email.com](mailto:ana@email.com);[ana@empresa.com](mailto:ana@empresa.com) |

La columna **Correos** contiene dos valores distintos.

### Grupos repetitivos

Otro caso muy habitual consiste en crear varias columnas similares.

| Cliente | Telefono1 | Telefono2 | Telefono3 |
| --------- | ----------- | ----------- | ----------- |

Este diseño tampoco es recomendable.

Aunque técnicamente cada columna sea atómica, el conjunto representa un grupo repetitivo.

Además:

* limita el número máximo de teléfonos;
* obliga a dejar columnas vacías;
* dificulta el mantenimiento.

### La solución

Separar la información en una nueva tabla.

```text
CLIENTE

IdCliente
Nombre
```

```text
TELEFONO_CLIENTE

IdTelefono
Numero
IdCliente
```

Ahora un cliente puede tener uno, dos o veinte teléfonos sin modificar la estructura de la base de datos.

### ¿Qué NO exige la Primera Forma Normal?

Existe una idea equivocada muy extendida.

Muchos estudiantes creen que la Primera Forma Normal elimina toda la redundancia.

No es cierto.

Una tabla puede cumplir perfectamente la 1FN y seguir presentando dependencias parciales o transitivas.

Estas se resolverán en las siguientes formas normales.

### Nuestro caso práctico

En nuestra empresa comercial evitaremos desde el principio atributos como:

```text
ProductosComprados

Telefonos

Correos

CategoriasFavoritas
```

Cada uno de ellos se representará mediante tablas independientes relacionadas entre sí.

### Ideas clave

* La Primera Forma Normal exige valores atómicos.
* Cada celda debe contener un único dato.
* Deben evitarse listas dentro de una columna.
* Los grupos repetitivos suelen indicar un mal diseño.
* La 1FN constituye el punto de partida de la normalización.

