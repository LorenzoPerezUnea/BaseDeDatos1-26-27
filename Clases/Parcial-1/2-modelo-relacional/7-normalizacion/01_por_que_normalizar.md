# ¿Por qué normalizar?

Cuando comenzamos a diseñar una base de datos solemos preocuparnos por almacenar toda la información necesaria para que la aplicación funcione.

Sin embargo, almacenar la información no es suficiente.

También debemos hacerlo de manera que la base de datos sea fácil de mantener, consistente y capaz de evolucionar con el tiempo.

Aquí es donde aparece la normalización.

### Un problema muy común

Imaginemos que una empresa decide guardar toda la información de los pedidos en una única tabla.

| Pedido | Cliente | Dirección | Producto | Precio |
| -------- | --------- | ------------ | ---------- | -------: |
| 1      | Ana     | Calle A    | Ratón   |  18.90 |
| 1      | Ana     | Calle A    | Teclado  |  42.50 |
| 2      | Luis    | Calle B    | Ratón   |  18.90 |

A simple vista parece un diseño razonable.

Toda la información está disponible en una única tabla.

Sin embargo, observemos con atención.

El nombre del cliente aparece repetido.

La dirección también.

El precio del producto vuelve a repetirse.

Cuanto mayor sea la base de datos, mayor será la repetición.

### El verdadero problema

La redundancia no solo desperdicia espacio.

Provoca problemas mucho más graves.

Si el cliente cambia de dirección habrá que modificar todas las filas donde aparezca.

Si olvidamos actualizar una de ellas, la base de datos quedará inconsistente.

El mismo problema aparece con productos, empleados, proveedores y cualquier otra información repetida.

### El objetivo de la normalización

La normalización busca que cada dato se almacene una sola vez.

De esta forma:

* disminuye la redundancia;
* aumenta la consistencia;
* facilita el mantenimiento;
* reduce los errores.

No pretende complicar el modelo.

Pretende hacerlo más fiable.

### ¿Siempre debemos normalizar?

En la mayoría de aplicaciones empresariales, sí.

No obstante, como veremos al final de esta clase, existen situaciones en las que una pequeña desnormalización puede mejorar el rendimiento.

Por eso la normalización debe entenderse como una herramienta de diseño y no como una regla absoluta.

### Relación con las dependencias funcionales

La normalización no aparece de la nada.

Se basa directamente en las dependencias funcionales estudiadas en la clase anterior.

Ellas nos indican cuándo una tabla contiene información que realmente debería pertenecer a otra.

### Nuestro caso práctico

Durante esta clase partiremos deliberadamente de una base de datos mal diseñada.

La iremos refinando paso a paso aplicando cada Forma Normal hasta obtener un modelo limpio y profesional.

Este proceso permitirá comprender no solo el resultado final, sino también el motivo de cada transformación.

### Ideas clave

* Normalizar consiste en reorganizar una base de datos para mejorar su diseño.
* El principal objetivo es reducir redundancias.
* La redundancia provoca inconsistencias y dificulta el mantenimiento.
* Las dependencias funcionales indican cuándo una tabla necesita ser reorganizada.
* La normalización es un proceso progresivo basado en reglas bien definidas.

