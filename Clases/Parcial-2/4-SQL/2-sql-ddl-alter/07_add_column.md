# ADD COLUMN

## Introducción

Una de las modificaciones más habituales durante la evolución de una base de datos consiste en añadir nuevos atributos a una entidad ya existente.

Por ejemplo, imaginemos que inicialmente solo almacenábamos el nombre y el correo electrónico de cada cliente.

Tiempo después, el departamento comercial solicita registrar también el teléfono móvil.

No resulta necesario crear una nueva tabla ni eliminar la existente.

Simplemente añadiremos una nueva columna.

Esta operación se realiza mediante la cláusula **ADD COLUMN** de la sentencia `ALTER TABLE`.

---

### Sintaxis básica

La estructura general es la siguiente.

```sql
ALTER TABLE NombreTabla
ADD COLUMN NombreColumna TipoDato;
```

La nueva columna se añadirá al final de la definición de la tabla.

---

### Añadiendo un teléfono al cliente

Nuestro modelo inicial es el siguiente.

```text
Cliente

IdCliente
Nombre
CorreoElectronico
Ciudad
FechaRegistro
Activo
```

Ahora queremos incorporar un número de teléfono.

Ejecutaremos:

```sql
ALTER TABLE Cliente
ADD COLUMN Telefono VARCHAR(20);
```

La operación finaliza prácticamente de forma inmediata.

Sin embargo, la estructura de la tabla ha cambiado.

---

### Verificando la modificación

Comprobemos el resultado.

```sql
DESC Cliente;
```

Obtendremos una salida similar.

| Field             |
| ------------------- |
| IdCliente         |
| Nombre            |
| CorreoElectronico |
| Ciudad            |
| FechaRegistro     |
| Activo            |
| Telefono          |

La nueva columna aparece al final de la tabla.

Además, todos los registros existentes conservarán su información.

Únicamente tendrán el valor `NULL` en la nueva columna hasta que se actualicen.

---

### Añadiendo varias columnas

También es posible incorporar varias columnas en una sola sentencia.

```sql
ALTER TABLE Cliente

ADD COLUMN Telefono VARCHAR(20),

ADD COLUMN CodigoPostal VARCHAR(10);
```

Esta sintaxis resulta especialmente útil cuando una nueva funcionalidad requiere ampliar considerablemente una tabla.

---

### Añadiendo columnas con restricciones

La nueva columna puede definirse exactamente igual que durante un `CREATE TABLE`.

Por ejemplo:

```sql
ALTER TABLE Cliente

ADD COLUMN FechaUltimoAcceso DATETIME,

ADD COLUMN PuntosFidelidad INT DEFAULT 0;
```

En este caso todos los clientes existentes comenzarán con cero puntos de fidelidad.

Los nuevos registros heredarán automáticamente dicho valor por defecto.

---

### Casos reales

A medida que avance nuestro caso práctico utilizaremos `ADD COLUMN` con frecuencia.

Por ejemplo, incorporaremos atributos como:

* teléfono;
* dirección de envío;
* límite de crédito;
* puntos de fidelización;
* fecha del último acceso;
* observaciones.

Esto permitirá que la base de datos evolucione sin necesidad de reconstruir todo el esquema.

---

### Errores frecuentes

Muchos estudiantes eliminan y vuelven a crear una tabla simplemente para añadir una nueva columna.

Otro error habitual consiste en olvidar comprobar cómo afecta la nueva columna a los registros ya existentes.

Siempre debemos recordar que una modificación estructural también afecta a los datos previamente almacenados.

### Ideas clave

* `ADD COLUMN` permite ampliar una tabla existente.
* No elimina los datos almacenados previamente.
* Las nuevas columnas pueden incorporar restricciones y valores por defecto.
* Los registros existentes reciben inicialmente `NULL` o el valor definido mediante `DEFAULT`.
* Esta operación será muy habitual durante la evolución de nuestro caso práctico.

