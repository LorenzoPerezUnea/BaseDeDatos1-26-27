# Errores frecuentes

## Introducción

Las restricciones y las modificaciones estructurales son herramientas extremadamente potentes. Precisamente por ello, también son una fuente frecuente de errores durante el desarrollo de aplicaciones.

En esta clase hemos aprendido que la estructura de una base de datos no es algo estático, sino que evoluciona continuamente. Sin embargo, cada cambio debe realizarse con cuidado para no comprometer la integridad de la información.

Los siguientes errores aparecen con mucha frecuencia tanto en estudiantes como en desarrolladores con poca experiencia.

---

### Error 1. Crear una clave foránea antes que la tabla referenciada

Supongamos que intentamos ejecutar:

```sql
ALTER TABLE Producto

ADD CONSTRAINT FK_Producto_Categoria

FOREIGN KEY (IdCategoria)

REFERENCES Categoria(IdCategoria);
```

Si la tabla `Categoria` todavía no existe, MySQL rechazará la operación.

**Regla general:** primero se crea la tabla padre y después la tabla hija.

---

### Error 2. Utilizar tipos de datos diferentes

Una clave foránea debe ser compatible con la clave primaria que referencia.

Por ejemplo, si `Categoria.IdCategoria` es un `INT`, la columna `Producto.IdCategoria` también deberá ser un `INT`.

Utilizar tipos distintos provoca errores al crear la relación.

---

### Error 3. Intentar crear una restricción sobre datos inconsistentes

Supongamos que ya existen productos con un `IdCategoria` igual a 99, pero dicha categoría nunca fue creada.

Si intentamos añadir la clave foránea, MySQL detectará la inconsistencia y rechazará la operación.

Antes de añadir restricciones conviene revisar y limpiar los datos existentes.

---

### Error 4. Utilizar CASCADE sin comprender sus consecuencias

`ON DELETE CASCADE` puede resultar muy útil, pero también extremadamente peligroso.

Eliminar accidentalmente un registro de la tabla padre puede provocar la eliminación automática de cientos o miles de registros relacionados.

Antes de utilizar acciones en cascada siempre debe analizarse cuidadosamente su impacto.

---

### Error 5. Modificar columnas sin comprobar las aplicaciones

Cambiar el nombre o el tipo de una columna puede afectar a consultas SQL, procedimientos almacenados, informes o aplicaciones que dependen de ella.

En proyectos profesionales cualquier modificación estructural debe coordinarse con el resto del sistema.

---

### Error 6. Eliminar columnas sin copia de seguridad

`DROP COLUMN` elimina definitivamente tanto la definición como todos los datos almacenados.

Antes de ejecutar operaciones destructivas es recomendable disponer de una copia de seguridad reciente.

En producción, esta práctica no es opcional: forma parte del procedimiento estándar de administración.

---

### Error 7. No verificar las modificaciones

Después de utilizar `ALTER TABLE`, muchos principiantes continúan trabajando sin comprobar el resultado.

Siempre es recomendable ejecutar:

```sql
DESC NombreTabla;
```

o bien:

```sql
SHOW CREATE TABLE NombreTabla;
```

Estas consultas permiten confirmar que la modificación se ha realizado exactamente como esperábamos.

---

## Ideas clave

* Las restricciones deben incorporarse sobre datos consistentes.
* Las claves primarias y foráneas deben utilizar tipos compatibles.
* Las operaciones destructivas requieren especial precaución.
* `CASCADE` debe utilizarse únicamente cuando su comportamiento sea el deseado.
* Verificar el resultado de cada modificación forma parte de las buenas prácticas profesionales.

