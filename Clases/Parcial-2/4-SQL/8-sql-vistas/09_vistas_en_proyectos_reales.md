# Vistas en proyectos reales

## Introducción

Hasta ahora hemos estudiado las vistas desde un punto de vista académico. Sin embargo, donde realmente demuestran su utilidad es en proyectos profesionales.

Es muy raro encontrar una aplicación empresarial de cierto tamaño que trabaje únicamente con tablas.

Normalmente, entre las aplicaciones y las tablas existe una capa formada por:

* vistas;
* procedimientos almacenados;
* funciones;
* permisos.

Esta capa simplifica el desarrollo y protege la base de datos frente a cambios futuros.

---

## Arquitectura habitual

En una pequeña aplicación el acceso puede ser directo:

```text
Aplicación

↓

Tablas
```

Pero en un sistema empresarial la arquitectura suele ser diferente.

```text
Aplicación

↓

Vistas

↓

Tablas
```

Las aplicaciones rara vez consultan directamente las tablas más importantes.

---

## Ejemplo: ERP

Imaginemos un sistema de gestión empresarial.

La información de un cliente puede encontrarse repartida entre:

* Cliente
* Pedido
* Factura
* Pago
* Dirección
* Comercial

Un desarrollador no quiere escribir continuamente consultas con cinco o seis `JOIN`.

En su lugar utiliza una vista:

```sql
SELECT *
FROM VistaResumenClientes;
```

Toda la complejidad queda encapsulada.

---

## Ejemplo: Dashboard de ventas

Un cuadro de mando necesita mostrar:

* ventas del día;
* ventas del mes;
* productos más vendidos;
* clientes con mayor facturación.

Cada indicador puede construirse mediante una vista distinta.

Posteriormente la aplicación únicamente consulta esas vistas.

---

## Ejemplo: Aplicación web

Supongamos una tienda online.

La página principal necesita mostrar:

* nombre del producto;
* precio;
* categoría;
* stock disponible.

En lugar de consultar varias tablas, la aplicación puede utilizar:

```sql
SELECT *
FROM VistaCatalogoProductos;
```

La aplicación queda desacoplada del diseño interno de la base de datos.

---

## Ventajas para el mantenimiento

Supongamos que el modelo de datos cambia.

La información del cliente pasa a almacenarse en dos tablas distintas.

Si las aplicaciones utilizan vistas:

* modificamos la vista;
* las aplicaciones continúan funcionando.

Si las aplicaciones consultan directamente las tablas:

* habrá que modificar todas las consultas del proyecto.

La diferencia en el coste de mantenimiento puede ser enorme.

---

## Trabajo en equipo

En proyectos grandes suelen intervenir:

* administradores de bases de datos;
* desarrolladores backend;
* desarrolladores frontend;
* analistas;
* equipos de Business Intelligence.

Las vistas permiten ofrecer a cada equipo exactamente la información que necesita sin obligarlo a conocer toda la estructura interna de la base de datos.

---

## ¿Siempre deben utilizarse?

No.

En aplicaciones pequeñas una consulta directa puede ser suficiente.

Las vistas aportan mayor valor cuando:

* existen muchas consultas repetidas;
* trabajan varios desarrolladores;
* la base de datos evoluciona con frecuencia;
* diferentes usuarios necesitan distintos niveles de acceso.

---

## Ideas clave

* Las vistas son muy habituales en aplicaciones empresariales.
* Reducen el acoplamiento entre las aplicaciones y las tablas.
* Facilitan el mantenimiento cuando cambia el modelo de datos.
* Simplifican el trabajo de equipos numerosos.
* Constituyen una buena práctica en proyectos medianos y grandes.

