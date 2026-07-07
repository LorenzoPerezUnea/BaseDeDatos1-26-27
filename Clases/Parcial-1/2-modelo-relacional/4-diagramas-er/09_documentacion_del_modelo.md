# Documentación del modelo

Un buen modelo de datos no termina cuando el diagrama está completo.

Si dentro de seis meses otro desarrollador observa el diagrama y no entiende por qué se tomaron determinadas decisiones, el proyecto tendrá un serio problema.

Por este motivo, todo modelo profesional debe ir acompañado de una ​**documentación técnica**​.

Documentar no consiste únicamente en guardar un archivo con el diagrama. Significa registrar las decisiones tomadas durante el análisis para que cualquier miembro del equipo pueda comprenderlas en el futuro.

### ¿Por qué documentar?

Durante el desarrollo de un proyecto se toman cientos de decisiones.

Por ejemplo:

* ¿Por qué una relación es 1:N y no N:M?
* ¿Por qué un atributo es obligatorio?
* ¿Por qué se eligió un identificador artificial?
* ¿Qué regla de negocio justifica una determinada restricción?

Si estas decisiones no se documentan, con el tiempo terminarán olvidándose.

### ¿Qué debe documentarse?

La documentación debe describir tanto el modelo como el razonamiento que hay detrás de él.

Habitualmente incluye:

* Objetivo del sistema.
* Alcance del modelo.
* Entidades.
* Atributos.
* Relaciones.
* Cardinalidades.
* Reglas de negocio.
* Suposiciones realizadas.
* Limitaciones conocidas.
* Cambios respecto a versiones anteriores.

No basta con guardar el diagrama.

También debe explicarse.

### Diccionario de datos

Uno de los documentos más importantes es el ​**diccionario de datos**​.

Se trata de una descripción organizada de todos los elementos del modelo.

Por ejemplo:

| Elemento   | Descripción                                  |
| ------------ | ----------------------------------------------- |
| Cliente    | Persona que realiza compras.                  |
| Producto   | Artículo disponible para la venta.           |
| Pedido     | Solicitud de compra realizada por un cliente. |
| Categoría | Clasificación de los productos.              |

Más adelante ampliaremos este documento incorporando tipos de datos, restricciones y claves.

### Registrar las reglas de negocio

Las reglas de negocio también deben quedar por escrito.

Por ejemplo:

* Todo pedido pertenece a un cliente.
* Un cliente puede no tener pedidos.
* Todo producto pertenece a una categoría.
* Un pedido debe contener al menos un producto.

Estas reglas son tan importantes como el propio diagrama.

### Control de versiones

Durante el desarrollo el modelo irá evolucionando.

Es recomendable conservar un historial de cambios indicando:

| Versión | Cambios                             |
| ---------- | ------------------------------------- |
| 1.0      | Modelo inicial.                     |
| 1.1      | Se añade la entidad Factura.       |
| 1.2      | Se incorpora LíneaPedido.          |
| 1.3      | Se modifican varias cardinalidades. |

Esto facilita comprender cómo ha evolucionado el sistema.

### Caso práctico

Nuestro proyecto en GitHub actuará precisamente como documentación del modelo.

Cada clase añadirá nuevos conceptos sin eliminar el trabajo realizado anteriormente.

De esta forma cualquier estudiante podrá recorrer la evolución completa del diseño desde el primer diagrama hasta la implementación final en MySQL.

### Ideas clave

* Un modelo profesional siempre debe documentarse.
* El diagrama por sí solo no explica las decisiones de diseño.
* El diccionario de datos es una pieza fundamental de la documentación.
* Las reglas de negocio deben quedar registradas explícitamente.
* Documentar facilita el mantenimiento y la evolución del sistema.

