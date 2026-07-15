# Análisis del modelo

## Introducción

Una vez comprendido el funcionamiento general de TechShop, el siguiente paso consiste en transformar la información obtenida durante las reuniones con el cliente en un modelo conceptual.

Esta fase es una de las más importantes de cualquier proyecto de bases de datos.

Los errores cometidos durante el análisis suelen propagarse al resto del desarrollo y, una vez implementada la base de datos, corregirlos puede resultar costoso.

El objetivo de este bloque no consiste todavía en escribir código SQL.

Primero debemos responder preguntas como:

- ¿Qué información debe almacenarse?
- ¿Qué representa cada entidad?
- ¿Cómo se relacionan entre sí?
- ¿Qué datos son realmente importantes?
- ¿Qué información no debería almacenarse?

En proyectos reales, esta fase suele implicar reuniones con usuarios, entrevistas, revisión de documentación y análisis de los procesos internos de la empresa.

## Objetivos del bloque

Al finalizar este bloque el estudiante deberá ser capaz de:

- Identificar correctamente las entidades del dominio.
- Diferenciar entidades de atributos.
- Detectar relaciones entre entidades.
- Proponer cardinalidades razonables.
- Identificar posibles claves primarias.
- Descubrir requisitos que no aparecen explícitamente en el enunciado.
- Justificar decisiones de diseño.

## Información disponible

Tras varias entrevistas con la dirección de TechShop se recopilan los siguientes requisitos.

### Clientes

Cada cliente:

- posee un identificador único;
- tiene nombre y apellidos;
- dispone de correo electrónico;
- puede registrar varias direcciones de envío;
- puede realizar numerosos pedidos;
- mantiene un historial de compras.

### Productos

Cada producto:

- pertenece a una categoría;
- puede ser suministrado por uno o varios proveedores;
- posee un precio;
- dispone de un stock disponible;
- puede encontrarse temporalmente sin existencias.

### Pedidos

Cada pedido:

- pertenece a un único cliente;
- contiene uno o varios productos;
- tiene una fecha;
- posee un estado;
- puede generar uno o varios pagos;
- finaliza con un envío.

### Empleados

La empresa dispone de varios departamentos.

Cada empleado:

- pertenece a un departamento;
- posee un supervisor (salvo la dirección);
- tiene fecha de contratación;
- desempeña un cargo.

### Proveedores

Cada proveedor:

- suministra distintos productos;
- dispone de datos de contacto;
- puede trabajar con varias categorías.

## Entidades candidatas

A partir del análisis inicial es posible proponer la siguiente lista de entidades.

- Cliente
- Dirección
- Pedido
- DetallePedido
- Producto
- Categoría
- Proveedor
- Empleado
- Departamento
- Pago
- Envío

Todavía no sabemos exactamente qué atributos tendrá cada una.

Ese trabajo se realizará posteriormente.

## Relaciones iniciales

Podemos comenzar identificando algunas relaciones evidentes.

```text
Cliente ----- Pedido

Pedido ----- DetallePedido

DetallePedido ----- Producto

Producto ----- Categoría

Producto ----- Proveedor

Empleado ----- Departamento

Pedido ----- Pago

Pedido ----- Envío
```

Este primer esquema únicamente pretende comprender el negocio.

Todavía no representa un modelo definitivo.

## Preguntas que debemos hacernos

Antes de comenzar el diseño conviene responder cuestiones como:

- ¿Puede un cliente tener varias direcciones?
- ¿Un pedido puede enviarse parcialmente?
- ¿Un producto puede cambiar de categoría?
- ¿Existen productos descatalogados?
- ¿Puede un proveedor suministrar el mismo producto que otro?
- ¿Es necesario conservar el historial de precios?

Muchas de estas preguntas aparecerán durante cualquier proyecto profesional.

## Ejercicio guiado 1 (Profesor)

Analiza las entidades propuestas anteriormente.

Para cada una indica:

- qué representa;
- por qué es una entidad y no un atributo;
- qué información general debería almacenar.

El profesor resolverá este ejercicio razonando cada decisión.

## Ejercicio guiado 2 (Profesor)

Construye un diagrama conceptual sencillo indicando únicamente:

- entidades;
- relaciones;
- cardinalidades aproximadas.

No es necesario definir todavía atributos.

## Ejercicios de aula

### Ejercicio 1

Clasifica los siguientes elementos indicando si deberían modelarse como entidad, atributo o relación.

- Precio.
- Cliente.
- Pedido.
- Dirección.
- Fecha de contratación.
- Departamento.
- Stock.
- Categoría.

Justifica cada respuesta.

### Ejercicio 2

Propón tres atributos para cada una de las siguientes entidades:

- Cliente.
- Producto.
- Pedido.
- Empleado.
- Proveedor.

### Ejercicio 3

¿Qué entidad utilizarías para almacenar las líneas de un pedido?

Explica por qué.

### Ejercicio 4

¿Puede existir una relación directa entre Cliente y Producto?

Justifica tu respuesta.

### Ejercicio 5

¿Qué ocurriría si elimináramos la entidad DetallePedido?

Analiza las consecuencias.

### Ejercicio 6

Propón una posible jerarquía de categorías para una tienda informática.

Ejemplo:

- Hardware
- Software
- Redes
- Periféricos

Continúa ampliando la estructura.

### Ejercicio 7

Identifica al menos tres relaciones de tipo uno a muchos.

### Ejercicio 8

Identifica al menos una posible relación muchos a muchos.

## Retos

### Reto 1

¿Qué nuevas entidades añadirías si TechShop comenzara a vender productos mediante suscripción?

### Reto 2

Diseña una posible entidad denominada "Valoración" que permita a los clientes puntuar productos.

Indica únicamente:

- finalidad;
- relaciones;
- atributos principales.

### Reto 3

Propón cómo almacenar promociones temporales sin modificar la estructura básica del modelo.

## Trabajo autónomo

1. Elaborar un diagrama entidad-relación preliminar.
2. Justificar todas las entidades incluidas.
3. Explicar por qué se han descartado otras alternativas.
4. Detectar posibles requisitos ambiguos.
5. Redactar preguntas que deberían plantearse al cliente antes de comenzar la implementación.

## Lista de comprobación

Antes de continuar deberías ser capaz de responder afirmativamente a las siguientes cuestiones.

- ¿Sé diferenciar claramente entidades y atributos?
- ¿He identificado correctamente las relaciones principales?
- ¿Comprendo por qué existe la entidad DetallePedido?
- ¿Soy capaz de justificar cada entidad del modelo?
- ¿He detectado posibles dudas que deberían aclararse con el cliente?

## Conclusiones

El análisis conceptual transforma una descripción informal del negocio en un conjunto estructurado de entidades y relaciones. Cuanto más completo sea este análisis, menor será el número de modificaciones necesarias durante la implementación.

En el siguiente bloque comenzaremos a traducir este modelo conceptual a un esquema relacional preparado para implementarse en MySQL.

