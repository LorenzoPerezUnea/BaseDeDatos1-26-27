# IS NULL

## Introducción

Hasta ahora todas las comparaciones realizadas suponían que las columnas contenían algún valor.

Sin embargo, en una base de datos real existen numerosos casos en los que un dato todavía no está disponible.

Por ejemplo:

* un cliente puede no haber indicado su teléfono;
* un empleado puede no tener asignado un supervisor;
* un pedido puede no tener aún fecha de entrega;
* un producto puede no disponer de descripción.

En estas situaciones aparece un concepto muy importante en SQL: el valor ​**`NULL`**​.

Comprender correctamente su significado resulta esencial para evitar errores en las consultas.

---

## ¿Qué significa NULL?

`NULL` no significa:

* cero;
* cadena vacía (`''`);
* falso (`FALSE`);
* espacio en blanco.

`NULL` significa simplemente:

> **valor desconocido o no disponible.**

Es decir, el dato no existe o todavía no se conoce.

---

## ¿Por qué no funciona "="?

Muchos principiantes intentan escribir:

```sql
SELECT *
FROM Cliente
WHERE Telefono = NULL;
```

Esta consulta ​**no funciona**​.

Del mismo modo, tampoco funciona:

```sql
WHERE Telefono <> NULL;
```

La razón es que `NULL` no representa un valor normal, sino la ausencia de información.

Por ello SQL proporciona operadores específicos para trabajar con él.

---

## IS NULL

Para localizar registros cuyo valor sea desconocido utilizamos:

```sql
SELECT *
FROM Cliente
WHERE Telefono IS NULL;
```

Resultado:

| Nombre        | Teléfono |
| --------------- | ----------- |
| Ana Ruiz      | NULL      |
| Javier Torres | NULL      |

Todos los registros cuyo teléfono todavía no ha sido registrado aparecerán en el resultado.

---

## IS NOT NULL

También podemos buscar aquellos registros cuyo dato sí está informado.

```sql
SELECT *
FROM Cliente
WHERE Telefono IS NOT NULL;
```

Resultado:

| Nombre         | Teléfono |
| ---------------- | ----------- |
| Luis Gómez    | 654123987 |
| Elena Sánchez | 612987456 |

Esta consulta resulta muy frecuente para comprobar la calidad de los datos almacenados.

---

## Aplicaciones reales

`IS NULL` aparece constantemente en bases de datos empresariales.

Algunos ejemplos:

* pedidos aún no entregados;
* facturas sin fecha de pago;
* empleados sin jefe asignado;
* clientes sin correo electrónico;
* productos sin imagen.

En todos estos casos el uso de `NULL` permite representar correctamente información todavía incompleta.

---

## NULL y las restricciones

Recordemos que una columna definida como:

```sql
NOT NULL
```

nunca podrá contener valores nulos.

Por tanto, realizar una consulta `IS NULL` sobre dicha columna normalmente devolverá un conjunto vacío.

Esto demuestra la estrecha relación entre el DDL (restricciones) y el DQL (consultas).

---

## Errores frecuentes

Los errores más habituales son:

* utilizar `= NULL` en lugar de `IS NULL`;
* confundir `NULL` con una cadena vacía;
* pensar que `NULL` equivale al número cero.

Comprender esta diferencia evita muchos problemas durante el desarrollo de aplicaciones.

---

## Ideas clave

* `NULL` representa un dato desconocido o inexistente.
* No debe compararse utilizando `=` o `<>`.
* Para consultar valores nulos se utiliza `IS NULL`.
* Para localizar valores existentes se utiliza `IS NOT NULL`.
* El tratamiento correcto de `NULL` es fundamental en cualquier base de datos profesional.

