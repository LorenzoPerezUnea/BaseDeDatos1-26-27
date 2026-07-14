# Buenas prácticas

## Introducción

Las vistas son fáciles de crear, pero una mala organización puede convertir una base de datos en un sistema difícil de mantener.

En proyectos profesionales es habitual encontrar decenas o incluso cientos de vistas. Por ello, es importante seguir una serie de buenas prácticas que faciliten su comprensión y reutilización.

---

## 1. Asignar nombres descriptivos

El nombre de una vista debe indicar claramente qué información proporciona.

Buenos ejemplos:

```text
VistaClientesActivos

VistaVentasMensuales

VistaCatalogoProductos

VistaPedidosPendientes
```

Poco recomendables:

```text
Vista1

Datos

ConsultaNueva

Prueba
```

Un nombre descriptivo evita tener que inspeccionar la consulta para entender su finalidad.

---

## 2. Evitar `SELECT *`

Aunque es posible escribir:

```sql
CREATE VIEW VistaProductos AS
SELECT *
FROM Producto;
```

es preferible indicar explícitamente las columnas:

```sql
CREATE VIEW VistaProductos AS
SELECT
    IdProducto,
    Nombre,
    Precio,
    Stock
FROM Producto;
```

Esto ofrece varias ventajas:

* hace la consulta más legible;
* evita incorporar nuevas columnas de forma accidental;
* reduce la cantidad de datos recuperados;
* facilita el mantenimiento cuando cambia la estructura de la tabla.

---

## 3. Crear vistas con un único propósito

Cada vista debería resolver un problema concreto.

Por ejemplo:

* catálogo de productos;
* clientes activos;
* ventas por cliente.

No es recomendable crear una vista enorme que intente servir para todos los informes de la empresa.

Las vistas pequeñas suelen ser más reutilizables.

---

## 4. No encadenar demasiadas vistas

Es posible crear una vista utilizando otra vista:

```text
Vista A

↓

Vista B

↓

Vista C

↓

Vista D
```

Aunque MySQL lo permite, un exceso de niveles dificulta el mantenimiento y puede afectar al rendimiento.

Siempre que sea posible, conviene mantener una estructura sencilla.

---

## 5. Documentar las vistas

En proyectos colaborativos es recomendable mantener documentación indicando:

* finalidad;
* tablas utilizadas;
* autor (si procede);
* fecha de creación;
* aplicaciones que la utilizan.

Esta información facilita el mantenimiento futuro.

---

## 6. Revisar el rendimiento

Una vista compleja puede contener:

* varios `JOIN`;
* subconsultas;
* funciones de agregación;
* filtros.

Antes de utilizarla masivamente conviene comprobar que su rendimiento es adecuado.

Las vistas simplifican el código, pero no eliminan el coste de ejecutar la consulta.

---

## 7. Pensar en la seguridad

Cuando una vista vaya a ser utilizada por usuarios externos o distintos departamentos:

* mostrar únicamente las columnas necesarias;
* evitar datos sensibles;
* combinarla con permisos adecuados.

Las vistas forman parte de la estrategia de seguridad de una aplicación.

---

## Recomendaciones finales

Antes de crear una vista pregúntate:

* ¿Realmente se reutilizará?
* ¿Tiene un nombre claro?
* ¿Incluye solo las columnas necesarias?
* ¿Su consulta es fácil de entender?
* ¿Podrá mantenerse fácilmente dentro de unos meses?

Si la respuesta es afirmativa, probablemente estás diseñando una buena vista.

---

## Ideas clave

* Utiliza nombres descriptivos.
* Evita `SELECT *`.
* Diseña vistas con un único propósito.
* No encadenes demasiadas vistas.
* Documenta y revisa periódicamente las vistas más importantes.
* Considera siempre el rendimiento y la seguridad.

