# ¿Qué es un procedimiento?

## Introducción

Hasta ahora, todas las consultas que hemos realizado tenían un objetivo concreto:

* obtener información (`SELECT`);
* insertar registros (`INSERT`);
* modificar datos (`UPDATE`);
* eliminar registros (`DELETE`).

Cada sentencia se ejecutaba de forma independiente y finalizaba inmediatamente después de producir su resultado.

Sin embargo, en una aplicación real es habitual que una única operación requiera ejecutar ​**varias instrucciones SQL consecutivas**​.

Por ejemplo, registrar un pedido puede implicar:

1. Comprobar que el cliente existe.
2. Verificar que hay suficiente stock.
3. Insertar el pedido.
4. Insertar los productos vendidos.
5. Actualizar el inventario.
6. Registrar la operación en una tabla de auditoría.

Ejecutar todas estas instrucciones manualmente sería poco práctico.

Para resolver este problema existen los ​**procedimientos almacenados**​.

---

## Definición

Un **procedimiento almacenado** (​*Stored Procedure*​) es un conjunto de instrucciones SQL almacenadas en la base de datos bajo un nombre.

Posteriormente pueden ejecutarse mediante una única instrucción.

```text
CALL NombreProcedimiento();
```

En cierto modo, un procedimiento es parecido a una función en un lenguaje de programación.

En lugar de escribir siempre las mismas instrucciones, las agrupamos y les damos un nombre.

---

## Una analogía

Imaginemos una cafetería.

Cada vez que un cliente pide un desayuno completo, el camarero no explica paso a paso lo que debe hacerse.

Simplemente indica:

```text
Desayuno Completo
```

La cocina ya conoce la secuencia:

* preparar café;
* tostar pan;
* añadir mantequilla;
* servir zumo;
* entregar cubiertos.

Con los procedimientos ocurre exactamente igual.

En lugar de enviar muchas instrucciones SQL, enviamos una sola llamada.

---

## Ventajas

Los procedimientos almacenados ofrecen numerosas ventajas.

### Reutilización

El mismo procedimiento puede utilizarse desde:

* aplicaciones web;
* aplicaciones móviles;
* programas de escritorio;
* herramientas administrativas.

---

### Centralización

Toda la lógica queda almacenada en un único lugar.

Si es necesario modificarla, solo cambiaremos el procedimiento.

---

### Menor tráfico entre aplicación y servidor

Sin procedimientos:

```text
Aplicación

↓

INSERT

↓

UPDATE

↓

SELECT

↓

DELETE
```

Con procedimientos:

```text
Aplicación

↓

CALL RegistrarPedido()
```

La comunicación resulta mucho más sencilla.

---

### Mayor seguridad

Podemos conceder permisos para ejecutar un procedimiento sin permitir el acceso directo a determinadas tablas.

Este aspecto es especialmente importante en aplicaciones empresariales.

---

## Diferencias respecto a una vista

Es frecuente confundir ambos conceptos.

| Vista                             | Procedimiento                       |
| ----------------------------------- | ------------------------------------- |
| Guarda una consulta               | Guarda varias instrucciones         |
| Se utiliza mediante`SELECT`   | Se ejecuta mediante`CALL`       |
| Está orientada a consultar datos | Está orientado a realizar procesos |
| No suele contener lógica         | Puede contener lógica compleja     |

Las vistas simplifican consultas.

Los procedimientos automatizan procesos.

---

## Algunos ejemplos

Podríamos crear procedimientos para:

* registrar un nuevo cliente;
* realizar una venta;
* actualizar el stock;
* calcular estadísticas;
* cerrar la facturación diaria;
* generar informes automáticos.

Todos ellos se ejecutarían mediante una única llamada.

---

## Ideas clave

* Un procedimiento es un conjunto de instrucciones SQL almacenadas.
* Se ejecuta mediante `CALL`.
* Permite automatizar procesos repetitivos.
* Centraliza la lógica de negocio.
* Facilita el mantenimiento de aplicaciones.

