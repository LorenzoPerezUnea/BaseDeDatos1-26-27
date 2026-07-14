# Convenciones de nomenclatura

## Introducción

Uno de los aspectos más infravalorados en el desarrollo de bases de datos es la elección de nombres.

Una consulta puede estar perfectamente optimizada y, sin embargo, resultar extremadamente difícil de comprender si utiliza nombres poco descriptivos.

Las convenciones de nomenclatura permiten que todos los desarrolladores de un proyecto escriban el código siguiendo los mismos criterios.

Esto aporta numerosas ventajas:

- Facilita el mantenimiento.
- Reduce errores.
- Mejora la legibilidad.
- Hace que el código sea predecible.
- Simplifica el aprendizaje de nuevos miembros del equipo.

Aunque MySQL permite utilizar prácticamente cualquier nombre válido, no todas las opciones son igualmente recomendables.

## Elegir nombres descriptivos

El nombre de una tabla debe representar claramente la entidad que almacena.

Buenos ejemplos:

```text
Cliente

Producto

Pedido

Empleado

Proveedor
```

Poco recomendables:

```text
Tabla1

Datos

Info

Registro

T
```

Un desarrollador debería comprender el propósito de una tabla únicamente leyendo su nombre.

## Nombrar correctamente las columnas

Las columnas también deben describir claramente la información que contienen.

Por ejemplo:

```text
FechaPedido

PrecioUnitario

Cantidad

Total

Email
```

Resultan mucho más descriptivas que:

```text
Dato1

Valor

CampoA

X

Y
```

## Mantener un estilo uniforme

Una organización debe escoger un criterio y aplicarlo de forma consistente.

Por ejemplo:

```text
FechaPedido
```

o

```text
fecha_pedido
```

Ambos estilos son válidos.

Lo importante es no mezclarlos.

Poco recomendable:

```text
FechaPedido

precio_unitario

TotalPedido

id_cliente
```

La falta de consistencia dificulta la lectura del esquema.

## Nombrar las claves primarias

Una práctica muy habitual consiste en utilizar:

```text
IdCliente

IdProducto

IdPedido

IdEmpleado
```

De esta forma resulta evidente cuál es la clave principal de cada tabla.

Otra alternativa muy utilizada es:

```text
ClienteId

ProductoId
```

Lo importante es mantener el mismo criterio en todo el proyecto.

## Nombrar las claves foráneas

Las claves foráneas deberían indicar claramente la tabla a la que hacen referencia.

Por ejemplo:

```text
IdCliente

IdProducto

IdEmpleado
```

Dentro de la tabla `Pedido` estos nombres permiten identificar inmediatamente las relaciones existentes.

## Alias descriptivos

Cuando una consulta incluye varias tablas resulta recomendable utilizar alias.

Por ejemplo:

```sql
SELECT
    cli.Nombre,
    ped.FechaPedido
FROM Cliente AS cli
JOIN Pedido AS ped
    ON cli.IdCliente = ped.IdCliente;
```

Alias como:

```text
cli

ped

emp

prod
```

resultan mucho más informativos que:

```text
a

b

c

x

y
```

Especialmente en consultas complejas.

## Nombrar índices

Los índices también deberían seguir una convención.

Por ejemplo:

```text
idx_cliente_email

idx_producto_categoria

idx_pedido_fecha
```

Con solo leer el nombre resulta posible identificar:

- Que se trata de un índice.
- La tabla.
- La columna principal.

## Nombrar restricciones

Las restricciones también pueden recibir nombres descriptivos.

Ejemplo:

```text
fk_pedido_cliente

fk_detalle_producto

chk_precio_positivo
```

Esto facilita enormemente la interpretación de mensajes de error y el mantenimiento del esquema.

## Evitar abreviaturas ambiguas

Abreviaturas como:

```text
cl

pd

dt

inf

tmp
```

pueden resultar difíciles de interpretar fuera del contexto original.

Siempre que sea posible conviene utilizar nombres completos o abreviaturas ampliamente aceptadas por el equipo.

## Documentar las convenciones

En proyectos grandes suele existir un documento que especifica:

- Cómo nombrar tablas.
- Cómo nombrar columnas.
- Cómo nombrar índices.
- Cómo nombrar claves.
- Cómo nombrar procedimientos almacenados.
- Cómo nombrar vistas.

Gracias a ello todo el proyecto mantiene una apariencia uniforme.

## Buenas prácticas

- Elegir nombres claros y descriptivos.
- Mantener un estilo uniforme.
- Utilizar alias significativos.
- Nombrar explícitamente índices y restricciones.
- Evitar abreviaturas poco claras.
- Documentar las convenciones adoptadas.

## Conclusiones

Una buena convención de nomenclatura mejora la calidad del código SQL tanto como una buena optimización. Los nombres adecuados facilitan la comprensión del esquema, reducen errores y hacen que el mantenimiento resulte mucho más sencillo.

## Ideas clave

- Los nombres deben describir claramente su propósito.
- La consistencia es más importante que el estilo elegido.
- Alias descriptivos mejoran la legibilidad.
- Índices y restricciones también deben seguir una convención.
- Un proyecto uniforme resulta más fácil de mantener y evolucionar.

