# Integridad referencial en MySQL

## Introducción

Hasta este momento hemos aprendido a crear claves primarias y claves foráneas.

Sin embargo, todavía no hemos respondido a la pregunta más importante.

**¿Qué ocurre cuando los datos cambian?**

Supongamos que un producto pertenece a una categoría.

¿Qué debería suceder si alguien intenta eliminar esa categoría?

¿Debe permitirse la operación?

¿Deben eliminarse automáticamente todos los productos?

¿Debe actualizarse la relación?

Responder correctamente a estas preguntas constituye el objetivo de la ​**integridad referencial**​.

---

### ¿Qué es la integridad referencial?

La integridad referencial es el conjunto de reglas que garantiza que las relaciones entre tablas permanezcan siempre coherentes.

En otras palabras, impide que existan referencias hacia registros inexistentes.

Por ejemplo:

```text
Categoria

IdCategoria = 3

        ▲

        │

Producto

IdCategoria = 3
```

Mientras exista el producto, la categoría referenciada también debe existir.

La base de datos será la encargada de garantizar esta condición.

---

### El problema

Imaginemos la siguiente situación.

```text
Categoria

3  Portátiles

Producto

15  Ultrabook   IdCategoria = 3
```

Ahora ejecutamos:

```sql
DELETE FROM Categoria
WHERE IdCategoria = 3;
```

¿Qué debería ocurrir?

Si MySQL permitiera esta operación, el producto seguiría haciendo referencia a una categoría inexistente.

La base de datos quedaría inconsistente.

---

### RESTRICT

El comportamiento más habitual consiste en impedir la eliminación.

```sql
FOREIGN KEY (IdCategoria)

REFERENCES Categoria(IdCategoria)

ON DELETE RESTRICT
```

En este caso MySQL devolverá un error y cancelará la operación.

La categoría únicamente podrá eliminarse cuando deje de estar siendo utilizada.

Esta suele ser la opción más segura en aplicaciones empresariales.

---

### CASCADE

Otra posibilidad consiste en eliminar automáticamente todos los registros relacionados.

```sql
ON DELETE CASCADE
```

En este caso, si desaparece una categoría, también desaparecerán todos los productos asociados.

Aunque puede resultar útil en determinadas situaciones, debe utilizarse con mucha precaución.

Una eliminación accidental podría propagarse por numerosas tablas.

---

### SET NULL

Existe una tercera alternativa.

```sql
ON DELETE SET NULL
```

Cuando desaparece el registro padre, la clave foránea pasa automáticamente a valer `NULL`.

Esta opción únicamente es posible cuando la columna permite valores nulos.

---

### ON UPDATE

La integridad referencial también afecta a las modificaciones.

Por ejemplo:

```sql
ON UPDATE CASCADE
```

Si cambiara el identificador de una categoría, todas las claves foráneas relacionadas se actualizarían automáticamente.

En nuestro curso utilizaremos identificadores artificiales mediante `AUTO_INCREMENT`, por lo que esta situación será poco frecuente.

Aun así, es importante comprender su funcionamiento.

---

### ¿Qué utilizaremos durante el curso?

En nuestro caso práctico seguiremos una filosofía conservadora.

Siempre que sea posible utilizaremos:

* `ON DELETE RESTRICT`
* `ON UPDATE RESTRICT`

Esto obliga a realizar las modificaciones de forma explícita y evita eliminaciones masivas accidentales.

Más adelante analizaremos escenarios donde otras estrategias resultan más apropiadas.

---

### Errores frecuentes

Muchos estudiantes creen que una clave foránea únicamente sirve para conectar tablas.

En realidad, su función principal consiste en proteger la coherencia del modelo.

También es habitual utilizar `CASCADE` sin analizar cuidadosamente sus consecuencias.

Finalmente, algunos principiantes eliminan registros directamente desde la tabla padre sin tener en cuenta las dependencias existentes.

### Ideas clave

* La integridad referencial garantiza la coherencia entre tablas relacionadas.
* Las claves foráneas impiden referencias hacia registros inexistentes.
* `RESTRICT`, `CASCADE` y `SET NULL` determinan el comportamiento ante eliminaciones o modificaciones.
* En este curso utilizaremos principalmente `RESTRICT` para evitar pérdidas accidentales de información.
* La integridad referencial constituye uno de los pilares fundamentales del modelo relacional.

