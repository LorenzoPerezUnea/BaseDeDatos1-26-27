# ¿Qué es una dependencia funcional?

Después de comprender por qué existen las dependencias, podemos introducir su definición formal.

Una **dependencia funcional** expresa que el valor de uno o varios atributos determina de forma única el valor de otro atributo.

Se representa mediante una flecha.

```text
A → B
```

Se lee:

> **A determina funcionalmente a B.**

O también:

> **B depende funcionalmente de A.**

### La intuición

Antes de pensar en fórmulas, imaginemos un ejemplo.

Supongamos la siguiente tabla.

| IdCliente | Nombre       |
| ----------: | -------------- |
|         1 | Ana López   |
|         2 | Carlos Ruiz  |
|         3 | Marta Gómez |

Si conocemos el identificador del cliente, conocemos automáticamente su nombre.

Podemos escribir:

```text
IdCliente → Nombre
```

No importa cuántas filas tenga la tabla.

La relación siempre será cierta.

### Otro ejemplo

En la tabla PRODUCTO:

| IdProducto | Nombre  | Precio |
| ------------ | --------- | -------: |
| 100        | Ratón  |  18.90 |
| 101        | Teclado |  42.50 |

Podemos afirmar:

```text
IdProducto → Nombre

IdProducto → Precio
```

Porque cada identificador corresponde a un único producto.

### Dependencia de varios atributos

En ocasiones un único atributo no basta.

Por ejemplo:

```text
(IdPedido, IdProducto) → Cantidad
```

Solo conociendo ambos valores podemos saber la cantidad comprada.

Ninguno de ellos por separado resulta suficiente.

### Lo importante no es el valor

Muchas personas creen que las dependencias dependen de los datos almacenados.

En realidad dependen del significado de esos datos.

Aunque hoy solo exista un cliente llamado Ana, no podemos afirmar:

```text
Nombre → IdCliente
```

Porque mañana podrían existir dos clientes con el mismo nombre.

Las dependencias se basan en las reglas del negocio, no en una coincidencia de los datos actuales.

### Notación habitual

A lo largo del resto del curso utilizaremos constantemente expresiones como:

```text
IdCliente → Nombre

IdCliente → Correo

IdPedido → Fecha

(IdPedido, IdProducto) → Cantidad
```

Esta notación será imprescindible para estudiar las Formas Normales.

### Ideas clave

* Una dependencia funcional indica que un conjunto de atributos determina otro.
* Se representa mediante la flecha ​**→**​.
* Las dependencias describen reglas del negocio.
* No dependen de los datos concretos almacenados.
* Constituyen el fundamento matemático de la normalización.

