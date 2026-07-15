# Creación del esquema

## Introducción

Una vez analizado el problema y definidas las entidades principales, llega el momento de convertir el modelo conceptual en un esquema relacional implementable en MySQL.

Hasta ahora hemos trabajado a un nivel relativamente abstracto.

A partir de este bloque comenzaremos a tomar decisiones concretas sobre:

- tablas;
- claves primarias;
- claves foráneas;
- tipos de datos;
- restricciones;
- nombres de columnas.

Este proceso debe realizarse cuidadosamente.

Una mala decisión en el diseño del esquema puede provocar problemas de rendimiento, redundancia de información o dificultades para ampliar la base de datos en el futuro.

## Objetivos del bloque

Al finalizar este bloque el estudiante será capaz de:

- Transformar entidades en tablas.
- Definir claves primarias.
- Identificar claves foráneas.
- Seleccionar tipos de datos adecuados.
- Aplicar restricciones de integridad.
- Justificar decisiones de diseño.

## Esquema propuesto

Durante el taller utilizaremos el siguiente conjunto de tablas.

```text
Departamento

Empleado

Cliente

Direccion

Categoria

Proveedor

Producto

ProductoProveedor

Pedido

DetallePedido

Pago

Envio
```

Este modelo permite representar la mayor parte de las operaciones habituales de una empresa de comercio electrónico.

## Relaciones principales

```text
Departamento

↓

Empleado

Cliente

↓

Pedido

↓

DetallePedido

↓

Producto

↓

Categoria

Producto

↕

Proveedor

Pedido

↓

Pago

Pedido

↓

Envio
```

Las relaciones muchos a muchos se resolverán mediante tablas intermedias cuando resulte necesario.

## Criterios de diseño

Durante la implementación seguiremos las siguientes normas.

### Claves primarias

Todas las tablas dispondrán de una clave primaria sencilla basada en un identificador numérico.

Ejemplo:

```text
id_cliente

id_producto

id_pedido
```

### Claves foráneas

Las relaciones se implementarán utilizando claves externas.

Por ejemplo:

```text
Pedido

id_cliente
```

### Nombres

Se utilizarán nombres descriptivos.

Correcto:

```text
fecha_pedido
```

Evitar:

```text
fp

dato1

valor
```

### Tipos de datos

Seleccionaremos el tipo más adecuado para cada atributo.

Ejemplos:

```text
INT

VARCHAR

DATE

DATETIME

DECIMAL

BOOLEAN
```

No todos los datos deben almacenarse como texto.

## Normalización

Durante el diseño intentaremos evitar:

- información duplicada;
- dependencias innecesarias;
- redundancia.

Siempre que sea posible seguiremos las reglas estudiadas durante el curso.

## Ejercicio guiado 1 (Profesor)

Diseñar completamente la tabla Cliente indicando:

- columnas;
- tipo de datos;
- clave primaria;
- restricciones.

Posteriormente justificar cada decisión.

## Ejercicio guiado 2 (Profesor)

Diseñar la tabla Pedido.

Explicar:

- relación con Cliente;
- restricciones necesarias;
- posibles índices futuros.

## Ejercicios de aula

### Ejercicio 1

Diseña la tabla Departamento.

### Ejercicio 2

Diseña la tabla Empleado.

### Ejercicio 3

Diseña la tabla Categoria.

### Ejercicio 4

Diseña la tabla Producto.

### Ejercicio 5

Diseña la tabla Proveedor.

### Ejercicio 6

Diseña la tabla ProductoProveedor.

### Ejercicio 7

Diseña la tabla DetallePedido.

### Ejercicio 8

Diseña la tabla Pago.

### Ejercicio 9

Diseña la tabla Envio.

### Ejercicio 10

Para cada tabla indica:

- clave primaria;
- claves foráneas;
- posibles restricciones UNIQUE;
- columnas NOT NULL.

## Retos

### Reto 1

¿Qué tablas podrían necesitar índices adicionales?

Justifica la respuesta.

### Reto 2

Diseña una tabla HistorialPrecio que permita conservar la evolución del precio de cada producto.

### Reto 3

Propón una estructura para almacenar cupones de descuento.

## Trabajo autónomo

1. Completar el diseño de todas las tablas.
2. Revisar que no existan redundancias.
3. Comprobar que todas las relaciones sean coherentes.
4. Preparar el esquema para implementarlo mediante SQL en el siguiente bloque.

## Lista de comprobación

- ¿Todas las entidades tienen una tabla?
- ¿Todas las tablas poseen clave primaria?
- ¿Las relaciones están correctamente representadas?
- ¿Los tipos de datos son adecuados?
- ¿El modelo resulta fácilmente ampliable?

## Conclusiones

El esquema relacional constituye el puente entre el análisis conceptual y la implementación física de la base de datos. Un diseño claro, consistente y bien documentado facilitará enormemente el desarrollo del resto del proyecto y permitirá construir consultas eficientes y fáciles de mantener.

