# DELETE

## Introducción

Hasta ahora hemos aprendido a crear nuevos registros mediante `INSERT` y a modificar información existente mediante `UPDATE`.

Sin embargo, durante la vida útil de una base de datos también será necesario eliminar información.

Un cliente puede solicitar la eliminación de su cuenta.

Un producto puede dejar de comercializarse.

Una categoría creada por error puede desaparecer.

Una tabla de pruebas puede necesitar ser limpiada.

Para todas estas situaciones SQL proporciona la sentencia ​**DELETE**​.

Aunque su sintaxis es sencilla, se trata de una de las instrucciones más delicadas de todo el lenguaje SQL, ya que elimina información que, en muchos casos, no podrá recuperarse.

---

## ¿Qué hace DELETE?

La sentencia `DELETE` elimina uno o varios registros de una tabla.

Es importante comprender que:

* elimina filas;
* no elimina columnas;
* no modifica la estructura de la tabla.

Visualmente:

```text
Antes

Cliente

1  Ana

2  Luis

3  Marta

↓

DELETE

↓

Cliente

1  Ana

3  Marta
```

La tabla sigue existiendo exactamente igual.

Únicamente ha disminuido el número de registros almacenados.

---

## Sintaxis general

La estructura básica es la siguiente.

```sql
DELETE FROM NombreTabla

WHERE Condición;
```

La condición determina exactamente qué registros serán eliminados.

---

## Primer ejemplo

Supongamos que un cliente solicita la eliminación de su cuenta.

```sql
DELETE FROM Cliente

WHERE IdCliente = 5;
```

Únicamente desaparecerá el cliente cuyo identificador sea 5.

Todos los demás permanecerán intactos.

---

## Eliminando varios registros

También podemos eliminar varios registros simultáneamente.

Por ejemplo, todos los productos inactivos.

```sql
DELETE FROM Producto

WHERE Activo = FALSE;
```

Cada fila que cumpla la condición será eliminada.

---

## Comprobando el resultado

Después de una eliminación siempre es recomendable verificar el contenido restante.

```sql
SELECT *
FROM Cliente;
```

De esta forma confirmamos que únicamente han desaparecido los registros esperados.

---

## DELETE y las claves foráneas

En las clases anteriores estudiamos la integridad referencial.

Esto afecta directamente a `DELETE`.

Supongamos que intentamos eliminar una categoría que todavía está siendo utilizada por varios productos.

```sql
DELETE FROM Categoria

WHERE IdCategoria = 1;
```

Si la clave foránea fue definida con:

```text
ON DELETE RESTRICT
```

MySQL impedirá la operación y mostrará un error.

Esto evita dejar productos apuntando a categorías inexistentes.

La integridad referencial protege automáticamente la coherencia de la base de datos.

---

## Eliminaciones masivas

También es posible eliminar una gran cantidad de registros.

Por ejemplo:

```sql
DELETE FROM Cliente

WHERE Activo = FALSE;
```

En una sola operación desaparecerán todos los clientes inactivos.

Este tipo de consultas debe ejecutarse siempre con extrema precaución.

---

## La importancia del WHERE

Al igual que ocurre con `UPDATE`, omitir la cláusula `WHERE` tiene consecuencias muy graves.

```sql
DELETE FROM Cliente;
```

Esta instrucción elimina **todos los registros** de la tabla.

La tabla seguirá existiendo, pero completamente vacía.

Más adelante dedicaremos un apartado completo a estudiar cómo evitar este tipo de errores.

---

## Casos reales

Algunos ejemplos habituales son:

* eliminar cuentas de prueba;
* borrar registros temporales;
* retirar productos descatalogados;
* limpiar tablas auxiliares;
* eliminar información duplicada.

En todos los casos conviene confirmar cuidadosamente qué registros van a desaparecer antes de ejecutar la operación.

---

## Errores frecuentes

El error más habitual consiste en olvidar la cláusula `WHERE`.

También es frecuente eliminar un registro padre sin tener en cuenta las restricciones de integridad referencial.

Finalmente, muchos principiantes ejecutan un `DELETE` sin comprobar previamente qué registros serán afectados.

Una buena práctica consiste en ejecutar primero un `SELECT` con la misma condición y verificar los resultados antes de realizar la eliminación.

### Ideas clave

* `DELETE` elimina filas, no tablas.
* La estructura de la tabla permanece intacta.
* La cláusula `WHERE` determina qué registros desaparecerán.
* Las claves foráneas pueden impedir determinadas eliminaciones.
* Antes de ejecutar un `DELETE` conviene comprobar cuidadosamente los registros afectados.

