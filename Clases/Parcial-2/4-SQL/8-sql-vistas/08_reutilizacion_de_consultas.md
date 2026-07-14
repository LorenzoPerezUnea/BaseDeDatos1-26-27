# Reutilización de consultas

## Introducción

Uno de los mayores beneficios de las vistas es la ​**reutilización del código SQL**​.

En proyectos pequeños quizá no parezca importante.

Sin embargo, en aplicaciones empresariales es habitual que una misma consulta sea utilizada por:

* aplicaciones web;
* aplicaciones móviles;
* informes;
* cuadros de mando (dashboards);
* procesos automáticos;
* herramientas de análisis.

Duplicar la misma consulta en todos esos lugares dificulta enormemente el mantenimiento del sistema.

Las vistas permiten escribir la consulta una sola vez y reutilizarla tantas veces como sea necesario.

---

## El problema del código duplicado

Supongamos que cinco informes diferentes necesitan mostrar las ventas junto con el nombre del cliente.

Sin vistas, los cinco informes contendrían una consulta similar a esta:

```sql
SELECT
    p.IdPedido,
    c.Nombre,
    p.Fecha,
    p.Total
FROM Pedido p
INNER JOIN Cliente c
ON p.IdCliente = c.IdCliente;
```

Si posteriormente cambia el modelo de datos, será necesario modificar las cinco consultas.

Esto incrementa el tiempo de mantenimiento y la posibilidad de introducir errores.

---

## La solución mediante vistas

Creamos una única vista:

```sql
CREATE VIEW VistaPedidosClientes AS
SELECT
    p.IdPedido,
    c.Nombre,
    p.Fecha,
    p.Total
FROM Pedido p
INNER JOIN Cliente c
ON p.IdCliente = c.IdCliente;
```

A partir de ese momento, cualquier informe utilizará simplemente:

```sql
SELECT *
FROM VistaPedidosClientes;
```

Toda la lógica queda centralizada en un único lugar.

---

## Una modificación sencilla

Supongamos que ahora queremos incluir también el correo electrónico del cliente.

Solo será necesario modificar la vista:

```sql
CREATE OR REPLACE VIEW VistaPedidosClientes AS
SELECT
    p.IdPedido,
    c.Nombre,
    c.Email,
    p.Fecha,
    p.Total
FROM Pedido p
INNER JOIN Cliente c
ON p.IdCliente = c.IdCliente;
```

Sin cambiar ninguna consulta adicional, todos los informes comenzarán a disponer del nuevo campo.

Esta es una de las mayores ventajas de las vistas.

---

## Vistas como capa de abstracción

Las vistas crean una separación entre:

* las tablas físicas;
* las aplicaciones que consumen los datos.

```text
Aplicación

↓

Vista

↓

Tablas
```

Gracias a esta capa intermedia, pequeños cambios en la estructura de la base de datos pueden gestionarse modificando únicamente la vista.

---

## En proyectos reales

En aplicaciones de gran tamaño es habitual encontrar:

* decenas de tablas;
* cientos de vistas;
* miles de consultas que utilizan esas vistas.

Este enfoque facilita enormemente el mantenimiento del sistema a largo plazo.

Por este motivo, las vistas forman parte del trabajo cotidiano de administradores de bases de datos y desarrolladores.

---

## Buenas prácticas

Para favorecer la reutilización:

* crea vistas con un objetivo bien definido;
* evita incluir información innecesaria;
* utiliza nombres descriptivos;
* documenta claramente el propósito de cada vista;
* reutiliza vistas existentes antes de crear nuevas.

---

## Ideas clave

* Las vistas eliminan la duplicación de consultas SQL.
* Centralizan la lógica de acceso a los datos.
* Facilitan el mantenimiento de aplicaciones grandes.
* Actúan como una capa de abstracción entre las aplicaciones y las tablas.
* Constituyen una de las herramientas más utilizadas en el desarrollo profesional de bases de datos.

