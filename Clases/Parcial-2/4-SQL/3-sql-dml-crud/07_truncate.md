# TRUNCATE

## Introducción

En el apartado anterior aprendimos que `DELETE` permite eliminar registros de una tabla.

Sin embargo, existe otra instrucción muy utilizada cuando el objetivo consiste en ​**vaciar completamente una tabla**​.

Esta instrucción recibe el nombre de ​**TRUNCATE**​.

Aunque el resultado pueda parecer similar al de un `DELETE` sin cláusula `WHERE`, existen importantes diferencias en cuanto a funcionamiento, rendimiento y uso profesional.

Comprender cuándo utilizar cada una de estas instrucciones evitará numerosos problemas en el futuro.

---

## ¿Qué hace TRUNCATE?

`TRUNCATE` elimina **todos los registros** de una tabla de una sola vez.

La estructura de la tabla permanece intacta.

Visualmente:

```text
Tabla Producto

120 registros

↓

TRUNCATE

↓

Tabla Producto

0 registros
```

Las columnas, restricciones, claves e índices continúan existiendo.

Únicamente desaparecen los datos.

---

## Sintaxis

Su sintaxis es extremadamente sencilla.

```sql
TRUNCATE TABLE Producto;
```

No utiliza la cláusula `WHERE`.

Siempre actúa sobre la totalidad de la tabla.

---

## Diferencias entre DELETE y TRUNCATE

Aunque ambos eliminan información, no deben considerarse equivalentes.

| DELETE                               | TRUNCATE                                       |
| -------------------------------------- | ------------------------------------------------ |
| Elimina filas seleccionadas o todas. | Elimina siempre todas las filas.               |
| Puede utilizar`WHERE`.           | No admite`WHERE`.                          |
| Elimina registro por registro.       | Vacía la tabla de forma mucho más eficiente. |
| Se utiliza para borrados selectivos. | Se utiliza para reiniciar tablas completas.    |

Esta diferencia será muy importante durante las prácticas.

---

## AUTO\_INCREMENT

Una diferencia especialmente relevante afecta a las columnas `AUTO_INCREMENT`.

Supongamos la siguiente situación.

Antes:

| IdProducto |
| -----------: |
|          1 |
|          2 |
|          3 |

Ejecutamos:

```sql
TRUNCATE TABLE Producto;
```

La tabla queda vacía.

Al insertar nuevamente un producto:

```sql
INSERT INTO Producto
(
    Nombre,
    Precio,
    Stock,
    Activo
)
VALUES
(
    'Nuevo portátil',
    950,
    10,
    TRUE
);
```

El nuevo identificador volverá a comenzar desde 1 (salvo configuraciones específicas del motor).

Este comportamiento difiere del de `DELETE`, donde normalmente el contador continúa aumentando.

---

## ¿Cuándo utilizar TRUNCATE?

Es especialmente útil para:

* reiniciar bases de datos de pruebas;
* comenzar una práctica desde cero;
* limpiar tablas temporales;
* vaciar información de demostración.

Durante este curso lo utilizaremos con frecuencia antes de volver a cargar el caso práctico completo.

---

## Restricciones

Si una tabla está siendo referenciada mediante claves foráneas, MySQL puede impedir el uso de `TRUNCATE`.

En esos casos será necesario eliminar previamente los registros relacionados o vaciar las tablas respetando el orden correcto.

La integridad referencial continúa aplicándose incluso durante operaciones masivas.

---

## Errores frecuentes

Uno de los errores más habituales consiste en utilizar `TRUNCATE` creyendo que solo eliminará algunos registros.

También es frecuente olvidar que no admite cláusulas `WHERE`.

Finalmente, muchos estudiantes utilizan `DELETE` para vaciar tablas muy grandes cuando `TRUNCATE` sería una opción considerablemente más eficiente.

### Ideas clave

* `TRUNCATE` vacía completamente una tabla.
* No elimina la estructura ni las restricciones.
* No admite la cláusula `WHERE`.
* Generalmente reinicia el contador `AUTO_INCREMENT`.
* Es la opción preferida para reiniciar tablas completas durante el desarrollo y las prácticas.

