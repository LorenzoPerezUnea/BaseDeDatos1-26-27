# PRIMARY KEY

## Introducción

En la clase anterior ya utilizamos la restricción `PRIMARY KEY` para identificar de forma única los registros de nuestras tablas.

Sin embargo, en aquel momento la presentamos simplemente como una parte de la sentencia `CREATE TABLE`.

Ahora estudiaremos esta restricción desde una perspectiva más profunda.

Comprenderemos qué ocurre internamente cuando MySQL define una clave primaria, por qué constituye uno de los pilares del modelo relacional y cómo influirá en todas las relaciones que construiremos a partir de este momento.

---

### Recordando el concepto

Una clave primaria identifica de forma única cada fila de una tabla.

Por definición:

* no admite valores duplicados;
* no admite valores nulos;
* cada tabla dispone de una única clave primaria, aunque esta pueda estar formada por varias columnas.

En nuestro proyecto utilizaremos claves primarias simples formadas por un único atributo identificador.

Por ejemplo:

| Tabla     | Clave primaria |
| ----------- | ---------------- |
| Cliente   | IdCliente      |
| Producto  | IdProducto     |
| Categoria | IdCategoria    |
| Empleado  | IdEmpleado     |

---

### Definición mediante CREATE TABLE

Recordemos el ejemplo utilizado en la clase anterior.

```sql
CREATE TABLE Cliente (

    IdCliente INT AUTO_INCREMENT PRIMARY KEY,

    Nombre VARCHAR(100) NOT NULL,

    CorreoElectronico VARCHAR(150) NOT NULL,

    Ciudad VARCHAR(80),

    FechaRegistro DATE,

    Activo BOOLEAN DEFAULT TRUE

);
```

Aunque la sintaxis es sencilla, MySQL realiza internamente varias operaciones.

No solo marca la columna como clave primaria.

También crea automáticamente un índice que permitirá localizar rápidamente cualquier registro mediante su identificador.

Más adelante, cuando estudiemos índices y optimización, comprenderemos la enorme importancia de este detalle.

---

### Verificando la clave primaria

Podemos comprobar la estructura de la tabla.

```sql
DESC Cliente;
```

Observaremos que la columna `Key` contiene el valor `PRI`.

También podemos obtener la definición completa de la tabla.

```sql
SHOW CREATE TABLE Cliente;
```

Esta instrucción resulta especialmente útil porque muestra exactamente cómo MySQL almacena internamente la definición del esquema.

---

### ¿Por qué utilizar identificadores artificiales?

Durante el diseño conceptual vimos que algunas entidades poseen atributos naturalmente únicos, como un DNI o un número de pasaporte.

Sin embargo, en nuestro proyecto utilizaremos identificadores artificiales.

Por ejemplo:

```text
IdCliente

IdProducto

IdPedido
```

Esta decisión aporta numerosas ventajas.

Si un cliente cambia de documento de identidad, la clave primaria permanece inalterada.

Del mismo modo, los identificadores no dependen de las reglas de negocio ni de la legislación de un país concreto.

Esto simplifica enormemente el mantenimiento de la base de datos.

---

### La base de las relaciones

En las próximas secciones aparecerá una nueva restricción: `FOREIGN KEY`.

Las claves foráneas siempre apuntarán hacia una clave primaria.

Por tanto, la clave primaria no solo identifica registros, sino que también actúa como punto de referencia para construir toda la red de relaciones entre las tablas del sistema.

Podemos imaginarla como el "ancla" sobre la que descansará el resto del modelo relacional.

---

### Errores frecuentes

Uno de los errores más habituales consiste en modificar el valor de una clave primaria después de que existan relaciones con otras tablas.

También es frecuente utilizar como clave primaria atributos cuyo valor puede cambiar con el tiempo.

En proyectos profesionales se recomienda que la clave primaria sea estable, sencilla y sin significado de negocio.

### Ideas clave

* La clave primaria identifica de forma única cada registro.
* MySQL crea automáticamente un índice asociado a la clave primaria.
* Durante este curso utilizaremos identificadores artificiales mediante `AUTO_INCREMENT`.
* Todas las claves foráneas apuntarán posteriormente hacia una clave primaria.
* La clave primaria constituye el eje central sobre el que se construye el modelo relacional.

