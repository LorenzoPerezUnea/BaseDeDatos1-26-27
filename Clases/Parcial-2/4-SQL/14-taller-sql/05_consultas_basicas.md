# Consultas básicas

## Introducción

Con la base de datos completamente implementada y poblada con información coherente, comienza la fase de explotación de los datos.

En un proyecto real, la mayor parte del tiempo que un desarrollador dedica a una base de datos consiste en consultar información.

Estas consultas pueden utilizarse para:

- mostrar información al usuario;
- generar informes;
- alimentar cuadros de mando;
- validar procesos internos;
- realizar análisis comerciales.

Aunque durante el curso ya hemos estudiado la sintaxis de `SELECT`, en este bloque se plantea un gran número de situaciones reales donde el estudiante deberá decidir qué información recuperar y cómo presentarla.

No todas las consultas tendrán una única solución.

En muchos casos será posible obtener el mismo resultado utilizando distintas estrategias.

## Objetivos del bloque

Al finalizar este bloque el estudiante será capaz de:

- Seleccionar información específica.
- Filtrar registros mediante condiciones.
- Ordenar resultados.
- Limitar el número de filas devueltas.
- Combinar múltiples criterios de búsqueda.
- Escribir consultas claras y fáciles de mantener.

## Recomendaciones

Antes de comenzar los ejercicios:

- analiza cuidadosamente el enunciado;
- identifica qué tablas intervienen;
- piensa si realmente necesitas todas las columnas;
- utiliza nombres descriptivos para los alias cuando resulte necesario;
- ordena los resultados para facilitar su interpretación.

## Ejercicio guiado 1 (Profesor)

Obtener un listado de todos los clientes mostrando:

- identificador;
- nombre completo;
- correo electrónico.

Ordenar alfabéticamente por apellidos.

El profesor resolverá la consulta explicando paso a paso el razonamiento seguido.

## Ejercicio guiado 2 (Profesor)

Mostrar todos los productos cuyo precio sea superior a un valor determinado.

Posteriormente modificar la consulta para devolver únicamente los diez productos más caros.

## Ejercicios de aula

### Bloque A. Selección simple

#### Ejercicio 1

Mostrar todos los departamentos.

#### Ejercicio 2

Listar todos los empleados.

#### Ejercicio 3

Mostrar todos los clientes.

#### Ejercicio 4

Mostrar todos los productos.

#### Ejercicio 5

Listar todos los proveedores.

#### Ejercicio 6

Mostrar todos los pedidos.

---

### Bloque B. Selección de columnas

#### Ejercicio 7

Mostrar únicamente el nombre y el precio de los productos.

#### Ejercicio 8

Mostrar nombre y correo de los clientes.

#### Ejercicio 9

Mostrar el nombre de los departamentos.

#### Ejercicio 10

Mostrar la fecha y el estado de todos los pedidos.

#### Ejercicio 11

Listar el nombre y teléfono de los proveedores.

---

### Bloque C. Filtrado

#### Ejercicio 12

Mostrar los productos con precio superior a 100 €.

#### Ejercicio 13

Mostrar los clientes registrados durante el último año.

#### Ejercicio 14

Obtener todos los pedidos en estado "Pendiente".

#### Ejercicio 15

Mostrar los productos cuyo stock sea inferior a diez unidades.

#### Ejercicio 16

Buscar empleados pertenecientes a un departamento concreto.

#### Ejercicio 17

Mostrar clientes cuyo apellido comience por la letra "G".

#### Ejercicio 18

Obtener productos cuyo nombre contenga la palabra "SSD".

---

### Bloque D. Ordenación

#### Ejercicio 19

Ordenar productos por precio ascendente.

#### Ejercicio 20

Ordenar clientes por apellidos y nombre.

#### Ejercicio 21

Ordenar pedidos desde el más reciente al más antiguo.

#### Ejercicio 22

Mostrar proveedores ordenados alfabéticamente.

---

### Bloque E. Limitación de resultados

#### Ejercicio 23

Mostrar los cinco productos más caros.

#### Ejercicio 24

Mostrar los diez clientes más recientes.

#### Ejercicio 25

Obtener los veinte primeros pedidos registrados.

---

### Bloque F. Condiciones múltiples

#### Ejercicio 26

Mostrar productos con precio superior a 300 € y stock inferior a cinco unidades.

#### Ejercicio 27

Buscar clientes registrados antes de una fecha determinada y que dispongan de correo electrónico.

#### Ejercicio 28

Obtener pedidos pendientes realizados durante el mes actual.

#### Ejercicio 29

Mostrar empleados pertenecientes a dos departamentos concretos.

#### Ejercicio 30

Buscar productos cuyo precio esté comprendido entre dos valores.

## Retos

### Reto 1

Escribe una consulta que devuelva todos los productos sin utilizar `SELECT *`.

### Reto 2

Reescribe tres ejercicios utilizando alias para mejorar la legibilidad.

### Reto 3

Intenta resolver todos los ejercicios empleando el menor número posible de columnas en la salida.

## Trabajo autónomo

1. Resolver todos los ejercicios pendientes.
2. Comprobar que cada consulta devuelve exactamente la información solicitada.
3. Analizar si existen varias soluciones posibles para algunos enunciados.
4. Documentar las consultas más interesantes.

## Lista de comprobación

- ¿Utilizo únicamente las columnas necesarias?
- ¿Las consultas están correctamente ordenadas?
- ¿Evito el uso innecesario de `SELECT *`?
- ¿Comprendo perfectamente cada cláusula utilizada?
- ¿Podría explicar el razonamiento seguido en cada consulta?

## Conclusiones

Las consultas básicas constituyen la herramienta más utilizada en el trabajo diario con bases de datos. Dominar operaciones sencillas de selección, filtrado y ordenación resulta imprescindible antes de abordar problemas más complejos basados en agregaciones, JOIN y subconsultas.

