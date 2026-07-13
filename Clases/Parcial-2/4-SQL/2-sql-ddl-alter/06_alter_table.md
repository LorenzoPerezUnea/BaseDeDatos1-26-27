# ALTER TABLE

## Introducción

Hasta este momento, cada vez que necesitábamos modificar una tabla la eliminábamos mediante `DROP TABLE` y la volvíamos a crear.

Este procedimiento resulta útil durante las primeras prácticas, cuando apenas existen datos almacenados. Sin embargo, en un entorno profesional sería una decisión desastrosa.

Imaginemos una empresa que lleva diez años registrando pedidos. Si fuera necesario añadir una nueva columna a la tabla `Pedido`, ¿sería razonable eliminar toda la tabla y perder millones de registros?

Evidentemente no.

Las bases de datos evolucionan continuamente. Se añaden nuevos requisitos, cambian las reglas de negocio y aparecen nuevas funcionalidades. Sin embargo, toda esa evolución debe realizarse ​**sin perder la información existente**​.

Para ello MySQL proporciona la sentencia ​**ALTER TABLE**​.

Podemos considerarla la herramienta de mantenimiento más importante del lenguaje DDL.

---

### ¿Qué es ALTER TABLE?

`ALTER TABLE` permite modificar la estructura de una tabla ya existente.

A diferencia de `CREATE TABLE`, que construye una tabla desde cero, `ALTER TABLE` actúa sobre una tabla que ya contiene información.

Gracias a esta sentencia podemos:

* añadir columnas;
* modificar columnas existentes;
* eliminar columnas;
* incorporar restricciones;
* renombrar columnas;
* cambiar el nombre de una tabla.

En esta clase estudiaremos las operaciones más habituales.

---

### ¿Por qué es tan importante?

Durante el desarrollo de un proyecto es completamente normal que el modelo de datos evolucione.

Por ejemplo, inicialmente nuestra empresa únicamente almacenaba el nombre y el correo electrónico de cada cliente.

Meses después surge un nuevo requisito.

Ahora también debe almacenarse el teléfono.

No necesitamos reconstruir la tabla.

Basta con modificar su definición.

Este tipo de cambios son extremadamente habituales en proyectos reales.

---

### Sintaxis general

La estructura básica es muy sencilla.

```sql
ALTER TABLE NombreTabla
Acción;
```

La acción dependerá del cambio que deseemos realizar.

Por ejemplo:

* añadir una columna;
* modificar su tipo de dato;
* eliminarla;
* añadir una restricción.

En los próximos capítulos estudiaremos cada uno de estos casos por separado.

---

### Comprobando el efecto de las modificaciones

Siempre que alteremos una tabla resulta recomendable comprobar inmediatamente su nueva estructura.

Las herramientas más utilizadas son:

```sql
DESC Cliente;
```

o bien

```sql
SHOW CREATE TABLE Cliente;
```

La primera ofrece una visión resumida de las columnas.

La segunda muestra la definición completa de la tabla exactamente como la interpreta MySQL.

Durante esta asignatura utilizaremos ambas con mucha frecuencia.

---

### ALTER TABLE en proyectos profesionales

En aplicaciones empresariales las modificaciones de una base de datos no suelen ejecutarse manualmente.

Lo habitual es utilizar herramientas de migración que generan automáticamente scripts `ALTER TABLE`.

Cada cambio queda registrado como una nueva versión del esquema.

De esta forma todos los servidores evolucionan exactamente igual.

Aunque en este curso realizaremos las modificaciones manualmente para comprender su funcionamiento, más adelante estudiaremos cómo estas herramientas automatizan el proceso.

---

### Errores frecuentes

Un error muy habitual consiste en utilizar `DROP TABLE` para realizar pequeños cambios en la estructura de una tabla.

También es frecuente modificar una tabla sin comprobar posteriormente el resultado mediante `DESC` o `SHOW CREATE TABLE`.

En proyectos profesionales cualquier modificación del esquema debe planificarse cuidadosamente, especialmente cuando existen millones de registros almacenados.

### Ideas clave

* `ALTER TABLE` permite modificar tablas existentes sin perder la información.
* Constituye una de las sentencias DDL más utilizadas en proyectos reales.
* Una base de datos evoluciona continuamente durante el desarrollo de una aplicación.
* Las modificaciones deben verificarse siempre después de ejecutarse.
* Los siguientes capítulos estudiarán las principales operaciones disponibles mediante `ALTER TABLE`.

