# Optimización

## Introducción

Una base de datos correctamente diseñada puede funcionar de manera excelente durante las primeras etapas de un proyecto.

Sin embargo, conforme aumenta el número de clientes, productos y pedidos, las consultas comienzan a procesar miles o incluso millones de registros. En ese momento aparecen nuevos desafíos relacionados con el rendimiento.

Una consulta que tarda unas pocas décimas de segundo sobre una base de datos pequeña puede necesitar varios segundos o incluso minutos cuando el volumen de información crece considerablemente.

Optimizar una base de datos no consiste únicamente en hacer que una consulta sea más rápida.

También implica:

- reducir el consumo de recursos;
- minimizar el tiempo de respuesta;
- facilitar la escalabilidad;
- mejorar la experiencia del usuario;
- disminuir los costes de infraestructura.

En este bloque se aplicarán los conocimientos adquiridos durante las clases dedicadas a índices, planes de ejecución y buenas prácticas para mejorar el rendimiento del proyecto TechShop.

## Objetivos del bloque

Al finalizar este bloque el estudiante será capaz de:

- Detectar consultas ineficientes.
- Interpretar planes de ejecución mediante `EXPLAIN`.
- Proponer índices adecuados.
- Reescribir consultas para mejorar su rendimiento.
- Justificar técnicamente las optimizaciones realizadas.

## Escenario de trabajo

Tras varios meses de funcionamiento, TechShop ha experimentado un crecimiento considerable.

La base de datos contiene aproximadamente:

| Tabla | Registros aproximados |
|--------|----------------------:|
| Cliente | 500 000 |
| Producto | 80 000 |
| Pedido | 12 000 000 |
| DetallePedido | 65 000 000 |
| Pago | 12 000 000 |
| Envío | 12 000 000 |

Los responsables de la empresa informan de que determinadas consultas utilizadas por el departamento comercial tardan demasiado en ejecutarse.

Nuestro objetivo consiste en localizar los problemas y proponer mejoras.

## Metodología de optimización

Antes de modificar una consulta se recomienda seguir siempre el mismo procedimiento.

1. Comprender el objetivo de la consulta.
2. Ejecutarla y medir su tiempo.
3. Analizar el plan mediante `EXPLAIN`.
4. Identificar el cuello de botella.
5. Aplicar una mejora.
6. Medir nuevamente el rendimiento.
7. Comparar los resultados.

Optimizar sin medir suele conducir a conclusiones erróneas.

## Ejercicio guiado 1 (Profesor)

Analizar una consulta lenta utilizando `EXPLAIN`.

Identificar:

- tipo de acceso;
- índice utilizado;
- número estimado de filas;
- operaciones de ordenación.

Posteriormente proponer una mejora y volver a medir el rendimiento.

## Ejercicio guiado 2 (Profesor)

Comparar dos versiones de una misma consulta.

La primera utilizará `SELECT *`.

La segunda devolverá únicamente las columnas necesarias.

Analizar las diferencias obtenidas.

## Ejercicios de aula

### Bloque A. EXPLAIN

#### Ejercicio 1

Ejecutar `EXPLAIN` sobre una consulta sencilla.

#### Ejercicio 2

Interpretar el tipo de acceso utilizado.

#### Ejercicio 3

Identificar posibles escaneos completos de tabla.

#### Ejercicio 4

Localizar consultas que no utilicen índices.

#### Ejercicio 5

Documentar las conclusiones.

---

### Bloque B. Índices

#### Ejercicio 6

Identificar columnas que deberían indexarse.

#### Ejercicio 7

Crear un índice sobre el correo electrónico de los clientes.

#### Ejercicio 8

Crear un índice sobre la fecha de los pedidos.

#### Ejercicio 9

Crear un índice compuesto para una consulta frecuente.

#### Ejercicio 10

Comparar el rendimiento antes y después de crear los índices.

---

### Bloque C. Reescritura de consultas

#### Ejercicio 11

Eliminar el uso innecesario de `SELECT *`.

#### Ejercicio 12

Simplificar una consulta con filtros redundantes.

#### Ejercicio 13

Reescribir una subconsulta utilizando un `JOIN`.

#### Ejercicio 14

Comparar ambas soluciones mediante `EXPLAIN`.

#### Ejercicio 15

Justificar cuál resulta preferible.

---

### Bloque D. Análisis global

#### Ejercicio 16

Seleccionar las cinco consultas más lentas del taller.

#### Ejercicio 17

Ordenarlas según prioridad de optimización.

#### Ejercicio 18

Proponer mejoras para cada una.

#### Ejercicio 19

Explicar el impacto esperado.

#### Ejercicio 20

Presentar un pequeño informe técnico.

## Retos

### Reto 1

Diseña un plan de optimización para una base de datos que haya duplicado su tamaño durante el último año.

### Reto 2

Identifica consultas cuya optimización pueda conseguirse modificando el modelo de datos en lugar de la propia consulta.

### Reto 3

Propón una estrategia para monitorizar continuamente el rendimiento de la base de datos.

## Trabajo autónomo

1. Resolver todos los ejercicios.
2. Comparar tiempos de ejecución antes y después de las mejoras.
3. Documentar los cambios realizados.
4. Justificar técnicamente todas las decisiones.

## Lista de comprobación

- ¿He utilizado `EXPLAIN` antes de optimizar?
- ¿Las mejoras propuestas están justificadas?
- ¿He comprobado el efecto de los índices?
- ¿Las consultas siguen siendo legibles?
- ¿He medido objetivamente el rendimiento?

## Conclusiones

La optimización constituye un proceso continuo basado en la observación, la medición y el análisis. Un desarrollador profesional no intenta adivinar qué consulta será más rápida, sino que utiliza herramientas objetivas para identificar problemas y evaluar el impacto real de cada mejora.

