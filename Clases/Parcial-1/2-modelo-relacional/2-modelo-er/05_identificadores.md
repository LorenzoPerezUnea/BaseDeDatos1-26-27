# Identificadores

En la clase anterior estudiamos las claves del Modelo Relacional.

Ahora nos encontramos todavía en la fase conceptual, donde aún no hablamos de claves primarias ni de tablas.

Sin embargo, incluso en esta etapa necesitamos una forma de distinguir unas entidades de otras.

Ese papel lo desempeñan los ​**identificadores**​.

### ¿Qué es un identificador?

Un identificador es un atributo, o conjunto de atributos, que permite distinguir de forma única cada instancia de una entidad.

Aunque posteriormente se transformará en una clave primaria, durante el modelado conceptual hablamos de identificadores.

### ¿Por qué son necesarios?

Imaginemos una empresa con miles de clientes.

Podrían existir varias personas llamadas:

* Ana López
* Carlos García
* María Fernández

Incluso podrían existir dos personas con exactamente el mismo nombre.

Por tanto, el nombre no basta para distinguirlas.

Necesitamos un identificador único.

### Ejemplo

La entidad **Cliente** podría definirse así:

```text
Cliente

IdCliente

Nombre

Apellidos

Teléfono
```

Aquí, **IdCliente** es el identificador.

Cada cliente tendrá un valor distinto.

### Identificadores naturales y artificiales

Existen dos grandes estrategias para identificar entidades.

| Tipo       | Ejemplo                                 |
| ------------ | ----------------------------------------- |
| Natural    | DNI, ISBN, matrícula, número de serie |
| Artificial | IdCliente, IdProducto, IdPedido         |

En la práctica, la mayoría de aplicaciones modernas utilizan identificadores artificiales porque permanecen estables incluso cuando cambian otros datos.

### ¿Puede haber varios candidatos?

Sí.

Por ejemplo, un empleado podría tener:

* DNI
* Número de empleado

Ambos podrían identificarlo de forma única.

Durante la implementación elegiremos cuál se convertirá en la clave primaria.

### Buenas características

Un buen identificador debería ser:

* Único.
* Estable.
* Obligatorio.
* Lo más sencillo posible.
* Independiente de cambios futuros.

Estas características facilitarán enormemente el mantenimiento de la base de datos.

### Caso práctico

En nuestra empresa utilizaremos identificadores artificiales para todas las entidades principales.

Por ejemplo:

| Entidad   | Identificador |
| ----------- | --------------- |
| Cliente   | IdCliente     |
| Producto  | IdProducto    |
| Empleado  | IdEmpleado    |
| Pedido    | IdPedido      |
| Factura   | IdFactura     |
| Proveedor | IdProveedor   |

Más adelante estos identificadores se convertirán en claves primarias dentro de MySQL.

### Ideas clave

* Un identificador distingue de forma única cada instancia de una entidad.
* En el modelo conceptual hablamos de identificadores; en el modelo relacional, de claves primarias.
* Los identificadores pueden ser naturales o artificiales.
* Deben ser únicos, estables y obligatorios.
* Elegir buenos identificadores simplifica todo el diseño posterior.

