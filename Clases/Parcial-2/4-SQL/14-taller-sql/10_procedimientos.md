# Procedimientos almacenados

## Introducción

Hasta ahora la mayor parte de las operaciones realizadas sobre la base de datos consistían en consultas o modificaciones puntuales.

Sin embargo, muchas aplicaciones necesitan ejecutar siempre la misma secuencia de instrucciones.

Por ejemplo:

- registrar un nuevo pedido;
- actualizar el inventario;
- calcular descuentos;
- generar un informe mensual;
- cancelar una compra.

Copiar estas operaciones dentro de la aplicación provoca duplicación de código y aumenta el riesgo de errores.

Los **procedimientos almacenados** permiten encapsular toda esa lógica dentro del propio servidor MySQL.

En este bloque construiremos varios procedimientos inspirados en situaciones habituales de TechShop.

## Objetivos del bloque

Al finalizar este bloque el estudiante será capaz de:

- Diseñar procedimientos reutilizables.
- Definir parámetros de entrada.
- Escribir lógica básica dentro de un procedimiento.
- Invocar procedimientos desde SQL.
- Identificar cuándo resulta conveniente utilizarlos.

## Recomendaciones

Antes de crear un procedimiento analiza:

- si la operación se repetirá con frecuencia;
- si puede reutilizarse desde distintas aplicaciones;
- si la lógica pertenece realmente a la base de datos;
- si facilita el mantenimiento del sistema.

## Ejercicio guiado 1 (Profesor)

Crear un procedimiento que permita registrar un nuevo cliente.

El procedimiento deberá recibir como parámetros:

- nombre;
- apellidos;
- correo electrónico;
- teléfono;
- fecha de registro.

Posteriormente comprobar que el nuevo cliente se ha insertado correctamente.

## Ejercicio guiado 2 (Profesor)

Crear un procedimiento que actualice el precio de un producto indicando:

- identificador;
- nuevo precio.

Analizar las ventajas frente a ejecutar directamente un `UPDATE`.

## Ejercicios de aula

### Bloque A. Inserción de información

#### Ejercicio 1

Crear un procedimiento para registrar un proveedor.

#### Ejercicio 2

Crear un procedimiento para insertar una categoría.

#### Ejercicio 3

Crear un procedimiento para añadir un producto.

#### Ejercicio 4

Crear un procedimiento para registrar un departamento.

#### Ejercicio 5

Crear un procedimiento para insertar un empleado.

---

### Bloque B. Actualización

#### Ejercicio 6

Crear un procedimiento para modificar el stock de un producto.

#### Ejercicio 7

Actualizar el estado de un pedido.

#### Ejercicio 8

Modificar el correo electrónico de un cliente.

#### Ejercicio 9

Actualizar el teléfono de un proveedor.

---

### Bloque C. Consultas encapsuladas

#### Ejercicio 10

Crear un procedimiento que devuelva todos los productos de una categoría.

#### Ejercicio 11

Mostrar todos los pedidos realizados por un cliente.

#### Ejercicio 12

Obtener los productos con stock inferior a un valor indicado.

#### Ejercicio 13

Mostrar los pedidos pendientes.

---

### Bloque D. Automatización

#### Ejercicio 14

Crear un procedimiento que aplique un descuento porcentual a todos los productos de una categoría.

#### Ejercicio 15

Diseñar un procedimiento que marque como cancelados todos los pedidos pendientes anteriores a una fecha determinada.

#### Ejercicio 16

Crear un procedimiento que genere un resumen del inventario.

## Retos

### Reto 1

Diseña un procedimiento que registre un pedido completo validando previamente que exista stock suficiente.

### Reto 2

Implementa comprobaciones para evitar precios negativos.

### Reto 3

Documenta todos los parámetros utilizados en los procedimientos creados.

## Trabajo autónomo

1. Implementar todos los procedimientos propuestos.
2. Probarlos utilizando distintos conjuntos de datos.
3. Documentar entradas y salidas.
4. Revisar el código para eliminar duplicaciones.

## Lista de comprobación

- ¿Cada procedimiento tiene un objetivo claro?
- ¿Los parámetros poseen nombres descriptivos?
- ¿Las validaciones son suficientes?
- ¿El código puede reutilizarse fácilmente?
- ¿La documentación explica correctamente su funcionamiento?

## Conclusiones

Los procedimientos almacenados permiten centralizar operaciones repetitivas y proporcionar una interfaz estable para interactuar con la base de datos. Cuando se diseñan adecuadamente reducen la duplicación de código y facilitan el mantenimiento de aplicaciones empresariales.

