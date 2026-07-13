# DROP COLUMN

## Introducción

Al igual que una base de datos puede crecer incorporando nuevos atributos, también puede simplificarse eliminando aquellos que ya no resultan necesarios.

Durante el desarrollo de una aplicación es relativamente frecuente descubrir que una columna nunca llegó a utilizarse, que fue sustituida por otra mejor diseñada o que una nueva versión del sistema ya no necesita almacenar determinada información.

En estas situaciones podemos eliminar la columna mediante la cláusula ​**DROP COLUMN**​.

Sin embargo, esta operación requiere mucha más precaución que las anteriores.

Una vez eliminada una columna, toda la información almacenada en ella desaparece.

---

### Sintaxis básica

La estructura general es:

```sql
ALTER TABLE NombreTabla
DROP COLUMN NombreColumna;
```

La operación elimina tanto la definición de la columna como todos los datos almacenados en ella.

No existe una "papelera de reciclaje" dentro de MySQL.

---

### Ejemplo

Supongamos que durante las primeras pruebas añadimos un atributo llamado `ObservacionesTemporales`.

```sql
ALTER TABLE Cliente
ADD COLUMN ObservacionesTemporales VARCHAR(300);
```

Tras varias semanas comprobamos que dicho campo nunca llegó a utilizarse.

Podemos eliminarlo mediante:

```sql
ALTER TABLE Cliente
DROP COLUMN ObservacionesTemporales;
```

La estructura de la tabla volverá a su estado anterior.

---

### Verificando la modificación

Como en todas las operaciones DDL, comprobaremos el resultado.

```sql
DESC Cliente;
```

La columna ya no aparecerá en la definición de la tabla.

También podemos utilizar:

```sql
SHOW CREATE TABLE Cliente;
```

para inspeccionar la estructura completa.

---

### ¿Qué ocurre con los datos?

Este aspecto merece especial atención.

Supongamos que la columna contenía miles de registros.

Después de ejecutar `DROP COLUMN`:

* desaparece la definición;
* desaparecen todos los valores almacenados;
* cualquier consulta que utilice esa columna dejará de funcionar.

Por este motivo, antes de eliminar una columna es recomendable realizar una copia de seguridad de la base de datos.

---

### Casos reales

En proyectos profesionales rara vez se elimina una columna inmediatamente.

Lo habitual consiste en seguir un proceso similar al siguiente:

1. dejar de utilizar la columna desde la aplicación;
2. comprobar durante un tiempo que realmente ya no es necesaria;
3. realizar una copia de seguridad;
4. eliminar finalmente la columna mediante un script de migración.

Este procedimiento reduce considerablemente el riesgo de pérdida de información.

---

### Errores frecuentes

Uno de los errores más habituales consiste en eliminar una columna sin comprobar si todavía está siendo utilizada por la aplicación.

También es frecuente olvidar que todas las consultas, informes y procedimientos almacenados que hagan referencia a esa columna deberán modificarse.

Por último, nunca debería eliminarse información importante sin disponer previamente de una copia de seguridad.

### Ideas clave

* `DROP COLUMN` elimina una columna existente.
* La información almacenada en ella también desaparece.
* Es una operación potencialmente destructiva.
* Siempre debe verificarse el impacto antes de ejecutarla.
* En proyectos profesionales suele formar parte de un proceso de migración cuidadosamente planificado.

