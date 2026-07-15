# Consultas con JOIN

## Introducción

Hasta este momento la mayoría de las consultas se han realizado sobre una única tabla.

Sin embargo, una base de datos relacional obtiene su verdadero potencial cuando es capaz de combinar información procedente de distintas tablas relacionadas.

Prácticamente cualquier aplicación empresarial necesita responder preguntas como:

- ¿Qué clientes realizaron cada pedido?
- ¿Qué productos contiene un pedido?
- ¿Qué empleado pertenece a cada departamento?
- ¿Qué proveedor suministra un determinado producto?

Responder a estas cuestiones exige utilizar operaciones `JOIN`.

En este bloque se trabajará intensivamente con este tipo de consultas mediante situaciones inspiradas en el funcionamiento diario de TechShop.

## Objetivos del bloque

Al finalizar este bloque el estudiante será capaz de:

- Identificar las tablas necesarias para una consulta.
- Elegir el tipo de JOIN adecuado.
- Combinar varias tablas en una misma consulta.
- Utilizar alias para mejorar la legibilidad.
- Resolver problemas empresariales mediante relaciones entre tablas.

## Recomendaciones

Antes de escribir una consulta:

1. Identifica qué información deseas obtener.
2. Localiza en qué tablas se encuentra.
3. Analiza las relaciones existentes.
4. Dibuja mentalmente el recorrido entre tablas si resulta necesario.

## Ejercicio guiado 1 (Profesor)

Mostrar un listado con:

- número de pedido;
- fecha;
- nombre del cliente.

Explicar cómo identificar la clave foránea adecuada y construir el `JOIN`.

## Ejercicio guiado 2 (Profesor)

Mostrar cada empleado junto con el nombre de su departamento.

Analizar por qué la información se encuentra distribuida en dos tablas distintas.

## Ejercicios de aula

### Bloque A. JOIN entre dos tablas

#### Ejercicio 1

Mostrar todos los pedidos junto con el cliente que los realizó.

#### Ejercicio 2

Listar todos los productos indicando su categoría.

#### Ejercicio 3

Mostrar empleados y departamentos.

#### Ejercicio 4

Obtener productos junto con sus proveedores.

#### Ejercicio 5

Mostrar pedidos junto con su envío correspondiente.

#### Ejercicio 6

Relacionar pedidos y pagos.

---

### Bloque B. JOIN entre tres tablas

#### Ejercicio 7

Mostrar:

- cliente;
- pedido;
- estado del envío.

#### Ejercicio 8

Mostrar:

- pedido;
- producto;
- cantidad.

#### Ejercicio 9

Obtener:

- producto;
- categoría;
- proveedor.

#### Ejercicio 10

Mostrar:

- empleado;
- departamento;
- supervisor.

#### Ejercicio 11

Listar:

- cliente;
- pedido;
- pago.

---

### Bloque C. JOIN múltiples

#### Ejercicio 12

Construir un informe que muestre para cada línea de pedido:

- cliente;
- número de pedido;
- producto;
- categoría;
- cantidad;
- precio.

#### Ejercicio 13

Mostrar el recorrido completo desde un proveedor hasta el cliente que compró uno de sus productos.

#### Ejercicio 14

Obtener un listado con:

- pedido;
- cliente;
- dirección;
- envío.

#### Ejercicio 15

Mostrar todos los productos vendidos junto con el proveedor correspondiente.

---

### Bloque D. JOIN con filtros

#### Ejercicio 16

Mostrar únicamente los pedidos realizados por un cliente concreto.

#### Ejercicio 17

Obtener productos de una categoría determinada junto con sus proveedores.

#### Ejercicio 18

Mostrar empleados pertenecientes a un departamento específico.

#### Ejercicio 19

Buscar todos los pedidos enviados durante el mes actual.

#### Ejercicio 20

Mostrar únicamente los productos cuyo proveedor pertenezca a un país determinado (añade el atributo si fuera necesario).

---

### Bloque E. Diseño de consultas

#### Ejercicio 21

Escribe una consulta que combine al menos cuatro tablas.

#### Ejercicio 22

Escribe otra consulta utilizando cinco tablas.

#### Ejercicio 23

Reescribe una consulta compleja utilizando alias descriptivos.

#### Ejercicio 24

Identifica posibles mejoras de legibilidad.

#### Ejercicio 25

Explica verbalmente el recorrido realizado por cada JOIN.

## Retos

### Reto 1

Construye una consulta que recorra el mayor número posible de tablas sin producir resultados redundantes.

### Reto 2

Diseña un informe comercial donde aparezcan conjuntamente clientes, pedidos, productos, proveedores y categorías.

### Reto 3

Analiza si alguna consulta podría simplificarse modificando el diseño de la base de datos. Justifica la respuesta.

## Trabajo autónomo

1. Resolver todos los ejercicios pendientes.
2. Dibujar el recorrido entre tablas antes de escribir las consultas más complejas.
3. Revisar el uso de alias.
4. Comparar varias soluciones para un mismo problema.

## Lista de comprobación

- ¿Identifico correctamente las claves foráneas?
- ¿Comprendo el recorrido entre tablas?
- ¿Utilizo únicamente los JOIN necesarios?
- ¿Las consultas son legibles?
- ¿Puedo explicar el resultado obtenido sin ejecutar la consulta?

## Conclusiones

Los `JOIN` constituyen una de las herramientas más potentes del modelo relacional. Dominar su utilización permite reconstruir información distribuida entre múltiples tablas y responder a preguntas empresariales que no podrían resolverse trabajando sobre tablas aisladas. En el siguiente bloque ampliaremos estas capacidades utilizando subconsultas y vistas para resolver problemas todavía más complejos.

