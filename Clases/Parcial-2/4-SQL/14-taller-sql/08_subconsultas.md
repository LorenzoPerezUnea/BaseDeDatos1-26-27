# Subconsultas

## Introducción

En numerosas ocasiones una consulta necesita utilizar el resultado de otra consulta para poder responder a una determinada pregunta.

Por ejemplo:

- ¿Qué clientes han realizado más pedidos que la media?
- ¿Qué productos tienen un precio superior al precio medio de su categoría?
- ¿Qué empleados pertenecen al departamento con mayor número de trabajadores?
- ¿Qué clientes nunca han realizado un pedido?

Estas preguntas pueden resolverse mediante **subconsultas**.

Durante el curso ya se estudiaron las distintas variantes de subconsultas y sus características. En este bloque el objetivo es utilizarlas dentro de un contexto empresarial real, comparando además cuándo una subconsulta es la mejor opción y cuándo resulta preferible utilizar un `JOIN`.

## Objetivos del bloque

Al finalizar este bloque el estudiante será capaz de:

- Resolver problemas utilizando subconsultas.
- Seleccionar el tipo de subconsulta adecuado.
- Combinar subconsultas con operadores de comparación.
- Utilizar `EXISTS`, `IN`, `ANY` y `ALL` cuando resulte apropiado.
- Comparar distintas soluciones para un mismo problema.

## Recomendaciones

Antes de utilizar una subconsulta pregúntate:

- ¿Necesito realmente una subconsulta?
- ¿Podría resolver el problema mediante un JOIN?
- ¿La consulta será fácil de mantener?
- ¿Existe una alternativa más eficiente?

En proyectos reales la consulta más corta no siempre es la mejor.

## Ejercicio guiado 1 (Profesor)

Obtener los productos cuyo precio sea superior al precio medio de todos los productos.

Analizar:

- la subconsulta;
- la consulta principal;
- el orden lógico de ejecución.

## Ejercicio guiado 2 (Profesor)

Mostrar los clientes que todavía no han realizado ningún pedido.

Comparar dos posibles soluciones:

- utilizando `NOT IN`;
- utilizando `NOT EXISTS`.

Analizar ventajas e inconvenientes.

## Ejercicios de aula

### Bloque A. Subconsultas simples

#### Ejercicio 1

Mostrar el producto más caro.

#### Ejercicio 2

Mostrar el producto más barato.

#### Ejercicio 3

Obtener todos los productos cuyo precio sea superior a la media.

#### Ejercicio 4

Mostrar los pedidos cuyo importe sea superior al importe medio.

#### Ejercicio 5

Listar los clientes registrados antes del cliente más reciente.

---

### Bloque B. Subconsultas con IN

#### Ejercicio 6

Mostrar los clientes que hayan realizado algún pedido.

#### Ejercicio 7

Obtener los productos vendidos al menos una vez.

#### Ejercicio 8

Mostrar las categorías que contienen productos vendidos.

#### Ejercicio 9

Listar proveedores que suministren productos vendidos.

#### Ejercicio 10

Mostrar empleados pertenecientes a departamentos con más de cinco trabajadores.

---

### Bloque C. EXISTS

#### Ejercicio 11

Mostrar clientes que tengan pedidos.

#### Ejercicio 12

Mostrar productos que nunca hayan sido vendidos.

#### Ejercicio 13

Obtener proveedores que todavía no suministren ningún producto.

#### Ejercicio 14

Mostrar categorías sin productos asociados.

---

### Bloque D. Subconsultas correlacionadas

#### Ejercicio 15

Mostrar los productos cuyo precio sea superior a la media de su propia categoría.

#### Ejercicio 16

Obtener los clientes cuyo número de pedidos sea superior a la media de pedidos por cliente.

#### Ejercicio 17

Mostrar los empleados cuyo salario sea superior a la media de su departamento (añade el atributo salario si fuera necesario).

#### Ejercicio 18

Calcular el pedido con mayor importe para cada cliente.

---

### Bloque E. Comparación de soluciones

#### Ejercicio 19

Resolver un mismo problema utilizando una subconsulta y un JOIN.

#### Ejercicio 20

Comparar la legibilidad de ambas soluciones.

#### Ejercicio 21

Analizar cuál sería más eficiente utilizando `EXPLAIN`.

#### Ejercicio 22

Justificar la elección final.

## Retos

### Reto 1

Construye una consulta que combine varias subconsultas anidadas.

### Reto 2

Reescribe una consulta compleja evitando completamente las subconsultas.

### Reto 3

Diseña una consulta que utilice simultáneamente `EXISTS` y una función de agregación.

## Trabajo autónomo

1. Resolver todos los ejercicios.
2. Comparar cada solución con una versión basada en `JOIN`.
3. Analizar el plan de ejecución cuando sea posible.
4. Documentar las diferencias encontradas.

## Lista de comprobación

- ¿Sé cuándo utilizar una subconsulta?
- ¿Comprendo la diferencia entre `IN` y `EXISTS`?
- ¿Soy capaz de interpretar una subconsulta correlacionada?
- ¿Puedo justificar la solución elegida?
- ¿He comprobado el rendimiento de las consultas más complejas?

## Conclusiones

Las subconsultas permiten resolver numerosos problemas de forma elegante y expresiva. Sin embargo, deben utilizarse con criterio, ya que en determinadas situaciones un `JOIN` o una reestructuración de la consulta puede proporcionar una solución más eficiente y fácil de mantener.

