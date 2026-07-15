# Consultas con agregación

## Introducción

En aplicaciones reales rara vez basta con recuperar registros individuales.

Los responsables de una empresa necesitan responder preguntas como:

- ¿Cuántos pedidos se han realizado este mes?
- ¿Cuál es el importe medio de las compras?
- ¿Qué categoría vende más?
- ¿Qué proveedor suministra más productos?
- ¿Cuántos clientes realizaron compras el último trimestre?

Este tipo de preguntas requiere utilizar funciones de agregación y operaciones de agrupamiento.

Durante el curso ya hemos estudiado `COUNT()`, `SUM()`, `AVG()`, `MIN()`, `MAX()`, `GROUP BY` y `HAVING`.

En este bloque el objetivo consiste en utilizarlas para resolver problemas empresariales reales.

## Objetivos del bloque

Al finalizar este bloque el estudiante será capaz de:

- Contar registros.
- Calcular sumas y promedios.
- Obtener valores máximos y mínimos.
- Agrupar información correctamente.
- Filtrar grupos mediante `HAVING`.
- Elaborar informes estadísticos sencillos.

## Recomendaciones

Antes de escribir una consulta pregúntate:

- ¿Qué quiero contar?
- ¿Qué quiero agrupar?
- ¿Necesito filtrar registros antes o después del agrupamiento?
- ¿Qué función de agregación resulta más adecuada?

## Ejercicio guiado 1 (Profesor)

Calcular el número total de clientes registrados.

Posteriormente modificar la consulta para contar únicamente los clientes que hayan realizado al menos un pedido.

El profesor explicará por qué ambas consultas responden a preguntas distintas.

## Ejercicio guiado 2 (Profesor)

Calcular el precio medio de todos los productos.

Después obtener también:

- precio mínimo;
- precio máximo;
- número total de productos.

Analizar el resultado.

## Ejercicios de aula

### Bloque A. Funciones de agregación

#### Ejercicio 1

Calcular el número total de productos.

#### Ejercicio 2

Calcular el número de proveedores.

#### Ejercicio 3

Obtener el importe medio de los productos.

#### Ejercicio 4

Mostrar el producto más caro.

#### Ejercicio 5

Mostrar el producto más barato.

#### Ejercicio 6

Calcular el valor total del inventario suponiendo que:

Valor = Precio × Stock

---

### Bloque B. GROUP BY

#### Ejercicio 7

Contar cuántos productos existen en cada categoría.

#### Ejercicio 8

Calcular el precio medio por categoría.

#### Ejercicio 9

Mostrar el número de empleados por departamento.

#### Ejercicio 10

Calcular el número de pedidos por cliente.

#### Ejercicio 11

Obtener el importe medio de los pedidos agrupado por estado.

#### Ejercicio 12

Mostrar el número de productos suministrados por cada proveedor.

---

### Bloque C. HAVING

#### Ejercicio 13

Mostrar únicamente las categorías que tengan más de diez productos.

#### Ejercicio 14

Obtener clientes que hayan realizado más de cinco pedidos.

#### Ejercicio 15

Mostrar proveedores que suministren más de veinte productos.

#### Ejercicio 16

Listar departamentos con más de tres empleados.

#### Ejercicio 17

Mostrar únicamente categorías cuyo precio medio supere los 300 €.

---

### Bloque D. Informes comerciales

#### Ejercicio 18

Calcular el número de pedidos realizados por mes.

#### Ejercicio 19

Obtener el importe medio de los pedidos.

#### Ejercicio 20

Mostrar el número de clientes registrados cada año.

#### Ejercicio 21

Calcular el total de unidades vendidas por producto.

#### Ejercicio 22

Obtener el número de pedidos cancelados.

#### Ejercicio 23

Calcular el porcentaje de pedidos entregados respecto al total.

---

### Bloque E. Interpretación de resultados

#### Ejercicio 24

Analiza qué categorías parecen tener mayor éxito.

#### Ejercicio 25

¿Qué departamentos concentran más empleados?

#### Ejercicio 26

¿Qué proveedores parecen estratégicos para la empresa?

#### Ejercicio 27

¿Qué información adicional sería útil almacenar para realizar análisis más completos?

## Retos

### Reto 1

Diseña un informe que resuma el estado general de la empresa utilizando únicamente cinco consultas SQL.

### Reto 2

Construye una consulta que combine varias funciones de agregación en un único resultado.

### Reto 3

Propón tres indicadores (KPIs) que podrían mostrarse en un panel de control para la dirección de TechShop.

## Trabajo autónomo

1. Resolver todos los ejercicios pendientes.
2. Comparar distintas formas de escribir consultas de agregación.
3. Revisar el uso correcto de `WHERE` y `HAVING`.
4. Preparar un pequeño informe explicando los resultados obtenidos.

## Lista de comprobación

- ¿Comprendo la diferencia entre `WHERE` y `HAVING`?
- ¿Utilizo correctamente `GROUP BY`?
- ¿El resultado responde exactamente a la pregunta planteada?
- ¿Las funciones de agregación elegidas son las adecuadas?
- ¿Podría explicar el significado empresarial de cada consulta?

## Conclusiones

Las funciones de agregación permiten transformar grandes volúmenes de datos en información útil para la toma de decisiones. Dominar estas consultas constituye un paso imprescindible antes de abordar informes más complejos basados en múltiples tablas.

