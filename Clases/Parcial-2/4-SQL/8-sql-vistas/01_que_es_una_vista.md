# ¿Qué es una vista?

## Introducción

A medida que una base de datos crece, las consultas que realizan los usuarios y las aplicaciones se vuelven cada vez más complejas.

Por ejemplo, obtener un informe de ventas puede requerir:

* unir varias tablas mediante `JOIN`;
* realizar cálculos con funciones de agregación;
* aplicar filtros;
* utilizar subconsultas.

Escribir esa misma consulta una y otra vez resulta tedioso y aumenta la probabilidad de cometer errores.

Para resolver este problema SQL incorpora las **vistas** (​*Views*​).

Una vista permite guardar una consulta con un nombre para reutilizarla posteriormente como si fuera una tabla.

---

## Definición

Una **vista** es un objeto de la base de datos cuyo contenido está definido por una consulta `SELECT`.

Cuando consultamos una vista, MySQL ejecuta automáticamente esa consulta y devuelve el resultado.

Es importante comprender que, en la mayoría de los casos, ​**una vista no almacena los datos**​, sino únicamente la consulta que permite obtenerlos.

---

## Una analogía

Podemos pensar en una vista como un acceso directo.

Supongamos que tenemos un documento muy largo en nuestro ordenador.

En lugar de abrir varias carpetas cada vez, creamos un acceso directo en el escritorio.

El documento sigue estando en el mismo lugar.

El acceso directo simplemente facilita llegar hasta él.

Con las vistas ocurre algo parecido.

Los datos siguen almacenados en las tablas originales.

La vista únicamente proporciona una forma más cómoda de acceder a ellos.

---

## Tablas frente a vistas

| Tabla                           | Vista                                         |
| --------------------------------- | ----------------------------------------------- |
| Almacena datos físicamente     | No almacena datos (normalmente)               |
| Ocupa espacio con los registros | Almacena únicamente la consulta              |
| Puede modificarse directamente  | Depende del tipo de vista                     |
| Contiene información real      | Muestra información obtenida de otras tablas |

Esta diferencia es fundamental y debe quedar clara desde el principio.

---

## Ejemplo conceptual

Supongamos las siguientes tablas:

```text
Cliente

Pedido

DetallePedido
```

Podemos construir una consulta:

```sql
SELECT
    c.Nombre,
    p.Fecha,
    p.Total
FROM Cliente c
JOIN Pedido p
ON c.IdCliente = p.IdCliente;
```

En lugar de escribir siempre esta consulta, podemos guardarla como una vista.

Después bastará con consultar:

```sql
SELECT *
FROM VistaPedidosClientes;
```

La vista actuará como si fuera una tabla.

---

## ¿Dónde se almacenan?

Las vistas forman parte del esquema de la base de datos.

Al igual que existen:

* tablas;
* índices;
* procedimientos;
* disparadores;

también existen vistas.

Si abrimos MySQL Workbench o phpMyAdmin podremos verlas dentro del listado de objetos de la base de datos.

---

## ¿Qué ocurre al consultar una vista?

Cuando escribimos:

```sql
SELECT *
FROM VistaClientes;
```

MySQL no busca datos dentro de la vista.

Internamente realiza un proceso similar a este:

```text
SELECT *

↓

Detecta que es una VIEW

↓

Obtiene la consulta almacenada

↓

La ejecuta

↓

Devuelve el resultado
```

Es decir, la vista funciona como una consulta previamente guardada.

---

## Ventajas iniciales

Las vistas ofrecen numerosas ventajas:

* reducen la cantidad de código SQL repetido;
* simplifican consultas complejas;
* facilitan el mantenimiento;
* permiten ocultar determinadas columnas;
* mejoran la organización del proyecto.

En los siguientes apartados iremos profundizando en cada una de estas ventajas.

---

## Ideas clave

* Una vista es una consulta almacenada con un nombre.
* Puede utilizarse igual que una tabla.
* Normalmente no almacena datos propios.
* Obtiene la información de una o varias tablas.
* Facilita enormemente el trabajo con consultas complejas.

