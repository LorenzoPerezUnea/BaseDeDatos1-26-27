# Errores frecuentes

## Introducción

Las vistas presentan una sintaxis sencilla, pero existen varios errores muy comunes durante su utilización.

Muchos de ellos no producen errores de compilación, sino resultados inesperados o problemas de mantenimiento.

Conocerlos permitirá evitar la mayoría de las incidencias habituales.

---

## Error 1. Pensar que una vista almacena datos

Es el error conceptual más frecuente.

Una vista ​**no contiene registros propios**​.

```text
Tabla

↓

Vista

↓

Consulta
```

Cada vez que consultamos la vista, MySQL ejecuta nuevamente la consulta almacenada.

---

## Error 2. Creer que mejora automáticamente el rendimiento

Muchos estudiantes piensan que:

```text
Consulta

↓

Vista

↓

Más rápida
```

Esto no es cierto.

La velocidad dependerá de:

* la consulta;
* los índices;
* el volumen de datos;
* el plan de ejecución.

La vista simplifica el código, pero no garantiza una mejora del rendimiento.

---

## Error 3. Utilizar `SELECT *`

Incorrecto:

```sql
CREATE VIEW VistaClientes AS
SELECT *
FROM Cliente;
```

Correcto:

```sql
CREATE VIEW VistaClientes AS
SELECT
    IdCliente,
    Nombre,
    Email
FROM Cliente;
```

Seleccionar únicamente las columnas necesarias mejora la claridad y facilita el mantenimiento.

---

## Error 4. Intentar modificar una vista no actualizable

Por ejemplo:

```sql
UPDATE VistaVentasClientes
SET TotalComprado = 5000;
```

Si la vista utiliza `GROUP BY` o funciones de agregación, MySQL generará un error porque no puede determinar qué fila debe modificarse.

---

## Error 5. Crear vistas demasiado complejas

Una vista con numerosos `JOIN`, subconsultas y cálculos puede resultar difícil de mantener.

Si una vista supera varias decenas de líneas, conviene revisar si puede simplificarse o dividirse en varias vistas más pequeñas.

---

## Error 6. No actualizar las vistas cuando cambia el modelo de datos

Si una tabla cambia de estructura:

* se elimina una columna;
* cambia un nombre;
* desaparece una tabla;

las vistas que dependan de ella pueden dejar de funcionar.

Después de cualquier modificación importante del esquema es recomendable revisar todas las vistas afectadas.

---

## Error 7. Utilizar nombres poco descriptivos

Nombres como:

```text
Vista1

VistaNueva

ConsultaFinal
```

dificultan enormemente el mantenimiento.

Es preferible utilizar nombres que describan claramente su contenido.

---

## Error 8. Duplicar vistas

En proyectos grandes puede ocurrir que varios desarrolladores creen vistas muy similares.

Antes de crear una nueva vista conviene comprobar si ya existe otra que pueda reutilizarse.

---

## Recomendaciones

Antes de crear una vista recuerda:

* definir claramente su objetivo;
* seleccionar únicamente las columnas necesarias;
* comprobar si será reutilizada;
* verificar si necesita ser actualizable;
* utilizar nombres claros y consistentes.

---

## Ideas clave

* Una vista no almacena datos.
* No garantiza una mejora del rendimiento.
* Evita utilizar `SELECT *`.
* No todas las vistas permiten modificaciones.
* Mantén las vistas sencillas, bien documentadas y fáciles de reutilizar.

