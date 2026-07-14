# ¿Por qué utilizar vistas?

## Introducción

Después de comprender qué es una vista, surge una pregunta natural:

> **Si ya puedo escribir consultas con `SELECT`, ¿para qué necesito una vista?**

La respuesta es sencilla:

Las vistas permiten trabajar de forma más eficiente cuando una consulta debe utilizarse repetidamente.

En proyectos profesionales es muy habitual que cientos de consultas compartan parte de su lógica.

Guardar esa lógica en una vista evita repetir código y facilita el mantenimiento de toda la aplicación.

---

## Problema 1. Repetición de consultas

Supongamos que continuamente necesitamos consultar los pedidos junto con el nombre del cliente.

Sin vistas tendríamos que escribir siempre:

```sql
SELECT
    c.Nombre,
    p.Fecha,
    p.Total
FROM Cliente c
INNER JOIN Pedido p
ON c.IdCliente = p.IdCliente;
```

Si esa consulta aparece en veinte informes distintos y posteriormente cambia el modelo de datos, habrá que modificar veinte consultas.

Con una vista, únicamente modificaremos un único objeto.

---

## Problema 2. Consultas demasiado largas

A medida que aumenta el número de tablas, también aumenta la longitud de las consultas.

Por ejemplo:

```text
Cliente

↓

Pedido

↓

DetallePedido

↓

Producto

↓

Categoría
```

Una consulta sencilla puede terminar ocupando varias decenas de líneas.

Si esa consulta se encapsula en una vista, el código utilizado por el desarrollador será mucho más simple.

---

## Problema 3. Mantenimiento

Imaginemos que el nombre de una columna cambia.

Sin vistas:

* hay que localizar todas las consultas;
* modificarlas;
* probarlas nuevamente.

Con vistas:

* se modifica únicamente la definición de la vista;
* todas las consultas que la utilizan continúan funcionando sin cambios.

Este aspecto resulta especialmente importante en aplicaciones grandes.

---

## Problema 4. Seguridad

No todos los usuarios necesitan acceder a todas las columnas de una tabla.

Por ejemplo:

La tabla `Empleado` podría contener:

* Nombre
* Cargo
* Salario
* Dirección
* Teléfono

Sin embargo, un usuario del departamento comercial quizá solo deba consultar:

* Nombre
* Cargo

Una vista permite mostrar únicamente esa información, ocultando el resto.

Más adelante dedicaremos un apartado completo a este uso.

---

## Problema 5. Reutilización

Una consulta bien diseñada puede utilizarse en:

* informes;
* aplicaciones web;
* aplicaciones móviles;
* cuadros de mando;
* herramientas de análisis.

En lugar de copiar y pegar la consulta en todos esos lugares, basta con reutilizar la vista.

---

## Un ejemplo sencillo

Sin vista:

```sql
SELECT
    c.Nombre,
    p.Total
FROM Cliente c
JOIN Pedido p
ON c.IdCliente = p.IdCliente;
```

Con vista:

```sql
SELECT *
FROM VistaVentasClientes;
```

El resultado es el mismo, pero el código resulta mucho más limpio y fácil de entender.

---

## ¿Las vistas mejoran el rendimiento?

Una duda frecuente es pensar que las vistas hacen que las consultas sean más rápidas.

En realidad, ​**no necesariamente**​.

Las vistas están pensadas principalmente para:

* organizar el código;
* reutilizar consultas;
* simplificar el desarrollo;
* mejorar la seguridad.

El rendimiento dependerá de la consulta que contenga la vista y de cómo el optimizador de MySQL la procese.

---

## Ideas clave

* Las vistas reducen la duplicación de consultas.
* Facilitan el mantenimiento de aplicaciones grandes.
* Simplifican consultas complejas.
* Favorecen la reutilización del código SQL.
* Constituyen una herramienta muy útil para organizar proyectos profesionales.

