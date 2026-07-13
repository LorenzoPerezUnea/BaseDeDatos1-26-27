# UNIQUE

## Introducción

La clave primaria garantiza que cada registro pueda identificarse de forma única dentro de una tabla. Sin embargo, en muchas ocasiones existen otros atributos que también deben ser únicos aunque no formen parte de la clave primaria.

Por ejemplo, en nuestra empresa dos clientes pueden tener nombres iguales, incluso vivir en la misma ciudad, pero ​**no deberían compartir la misma dirección de correo electrónico**​.

Del mismo modo:

* un proveedor podría tener un CIF único;
* un empleado un número de seguridad social único;
* un usuario un nombre de inicio de sesión único.

En todos estos casos necesitamos impedir valores duplicados sin convertir esos atributos en la clave primaria.

Para ello utilizaremos la restricción ​**UNIQUE**​.

---

### ¿Qué es UNIQUE?

La restricción `UNIQUE` obliga a que todos los valores almacenados en una columna sean diferentes.

Si intentamos insertar un valor que ya existe, MySQL rechazará la operación.

A diferencia de la clave primaria, una tabla puede tener varias restricciones `UNIQUE`.

Por ejemplo:

| Restricción | Cantidad por tabla |
| -------------- | -------------------- |
| PRIMARY KEY  | Una                |
| UNIQUE       | Varias             |

Esto permite proteger diferentes atributos que deben ser únicos.

---

### Aplicando UNIQUE

Supongamos que queremos garantizar que cada cliente tenga un único correo electrónico.

La tabla podría definirse así.

```sql
CREATE TABLE Cliente (

    IdCliente INT AUTO_INCREMENT PRIMARY KEY,

    Nombre VARCHAR(100) NOT NULL,

    CorreoElectronico VARCHAR(150) NOT NULL UNIQUE,

    Ciudad VARCHAR(80),

    FechaRegistro DATE,

    Activo BOOLEAN DEFAULT TRUE

);
```

Ahora MySQL comprobará automáticamente que ningún otro cliente utilice la misma dirección de correo.

---

### Probando la restricción

Insertemos un primer cliente.

```sql
INSERT INTO Cliente
(
    Nombre,
    CorreoElectronico
)
VALUES
(
    'Ana Ruiz',
    'ana@empresa.com'
);
```

Intentemos ahora insertar otro cliente utilizando el mismo correo.

```sql
INSERT INTO Cliente
(
    Nombre,
    CorreoElectronico
)
VALUES
(
    'Pedro López',
    'ana@empresa.com'
);
```

MySQL responderá con un error similar a:

```text
ERROR 1062 (23000)

Duplicate entry 'ana@empresa.com'
```

La segunda operación será cancelada automáticamente.

---

### UNIQUE y NULL

Existe una diferencia importante respecto a la clave primaria.

Una columna `UNIQUE` puede admitir valores `NULL`, siempre que no se combine con `NOT NULL`.

Por ejemplo:

```sql
Telefono VARCHAR(20) UNIQUE
```

En MySQL pueden existir varios registros cuyo teléfono sea `NULL`, ya que el valor desconocido no se considera un duplicado.

Sin embargo, si el atributo debe ser obligatorio y único, la definición habitual será:

```sql
CorreoElectronico VARCHAR(150)
NOT NULL
UNIQUE
```

Esta combinación es muy frecuente en aplicaciones empresariales.

---

### ¿Cuándo utilizar UNIQUE?

En nuestro caso práctico aparecerán numerosos ejemplos.

| Tabla     | Columna           |
| ----------- | ------------------- |
| Cliente   | CorreoElectronico |
| Usuario   | NombreUsuario     |
| Proveedor | CIF               |
| Empleado  | CorreoCorporativo |

Estos atributos identifican información que debe ser exclusiva, aunque no actúe como clave primaria.

---

### Casos reales

Las restricciones `UNIQUE` resultan especialmente importantes en sistemas donde diferentes usuarios pueden registrar información simultáneamente.

Aunque la aplicación valide previamente los datos, dos usuarios podrían intentar registrar el mismo correo electrónico exactamente al mismo tiempo.

La comprobación realizada por la propia base de datos evita este tipo de inconsistencias.

---

### Errores frecuentes

Muchos principiantes utilizan `PRIMARY KEY` para cualquier atributo único.

En realidad, la clave primaria identifica el registro completo, mientras que `UNIQUE` protege atributos adicionales.

También es frecuente olvidar combinar `UNIQUE` con `NOT NULL` cuando el dato debe ser obligatorio.

### Ideas clave

* `UNIQUE` impide almacenar valores duplicados.
* Una tabla puede contener varias restricciones `UNIQUE`.
* Es diferente de la clave primaria.
* Resulta ideal para correos electrónicos, nombres de usuario o documentos oficiales.
* La base de datos protege automáticamente la unicidad incluso cuando varios usuarios trabajan simultáneamente.

