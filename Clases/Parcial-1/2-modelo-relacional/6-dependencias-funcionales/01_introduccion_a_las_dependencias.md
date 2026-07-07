# Introducción a las dependencias

Hasta ahora hemos aprendido a construir tablas correctamente a partir del Modelo Entidad-Relación. Sin embargo, todavía queda una cuestión muy importante por resolver.

Imaginemos dos tablas diferentes.

Ambas almacenan exactamente la misma información.

Las dos funcionan.

Las dos permiten realizar consultas.

Entonces, ¿por qué una puede considerarse un buen diseño y la otra un mal diseño?

La respuesta está en las ​**dependencias funcionales**​.

### La información no es aleatoria

En una base de datos los valores no aparecen de forma independiente.

Existe una relación lógica entre muchos de ellos.

Por ejemplo, pensemos en un producto.

Si conocemos su identificador, automáticamente conocemos su nombre, su precio y su categoría.

No ocurre por casualidad.

Ocurre porque el negocio establece esa relación.

### Un ejemplo cotidiano

Consideremos la siguiente tabla.

| IdProducto | Nombre  | Precio |
| ------------ | --------- | -------: |
| 101        | Ratón  |  18.90 |
| 102        | Teclado |  42.50 |
| 103        | Monitor | 189.00 |

Si conocemos el valor ​**101**​, inmediatamente sabemos que corresponde al producto "Ratón".

No puede existir otro nombre distinto para ese mismo identificador.

Existe una dependencia entre ambos atributos.

### El origen de las dependencias

Las dependencias no son inventadas por el diseñador.

Provienen directamente de las reglas del negocio.

Por ejemplo:

* Cada cliente posee un identificador único.
* Cada pedido pertenece a un cliente.
* Cada producto tiene un precio actual.
* Cada categoría posee un nombre.

Estas reglas son las que generan las dependencias funcionales.

### ¿Para qué sirven?

Comprender las dependencias permitirá responder preguntas como:

* ¿Qué atributo identifica realmente una fila?
* ¿Existe información repetida?
* ¿Hay atributos innecesarios?
* ¿Puede dividirse una tabla?
* ¿Es posible eliminar redundancias?

Estas preguntas serán fundamentales durante la normalización.

### Nuestro caso práctico

Tomemos la tabla PRODUCTO.

```text
PRODUCTO

IdProducto
Nombre
Precio
Stock
IdCategoria
```

Sabemos que:

* el identificador determina el nombre;
* también determina el precio;
* también determina el stock;
* también determina la categoría.

Todas estas relaciones serán estudiadas formalmente durante esta clase.

### Ideas clave

* Los atributos de una tabla mantienen relaciones lógicas entre sí.
* Estas relaciones reciben el nombre de dependencias funcionales.
* Las dependencias proceden del negocio, no del sistema gestor.
* Constituyen la base matemática del diseño relacional.
* Sin comprender las dependencias resulta imposible normalizar correctamente una base de datos.

