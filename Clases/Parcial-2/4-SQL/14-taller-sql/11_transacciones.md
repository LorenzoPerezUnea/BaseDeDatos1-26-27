# Transacciones

## Introducción

En TechShop muchas operaciones afectan simultáneamente a varias tablas.

Por ejemplo, registrar un pedido implica:

1. Crear el pedido.
2. Insertar las líneas de detalle.
3. Descontar el stock.
4. Registrar el pago.
5. Generar el envío.

Si alguna de estas operaciones falla, la base de datos no puede quedar en un estado intermedio.

Imaginemos que se registra el pago pero no el pedido.

O que se descuenta el stock sin llegar a guardar la compra.

Estos errores provocarían inconsistencias muy graves.

Las **transacciones** garantizan que un conjunto de operaciones se ejecute como una única unidad lógica.

## Objetivos del bloque

Al finalizar este bloque el estudiante será capaz de:

- Diseñar operaciones transaccionales.
- Identificar situaciones donde deben utilizarse transacciones.
- Utilizar `BEGIN`, `COMMIT` y `ROLLBACK`.
- Analizar escenarios donde intervienen varios usuarios.
- Comprender la importancia de las propiedades ACID en aplicaciones reales.

## Recomendaciones

Antes de comenzar una transacción pregúntate:

- ¿Qué operaciones deben ejecutarse conjuntamente?
- ¿Qué ocurrirá si una de ellas falla?
- ¿Cómo recuperará el sistema una situación de error?
- ¿Qué datos podrían verse afectados por otros usuarios simultáneamente?

## Ejercicio guiado 1 (Profesor)

Diseñar una transacción que registre un nuevo pedido.

La operación deberá incluir:

- inserción del pedido;
- inserción de las líneas;
- actualización del stock.

Finalizar correctamente mediante `COMMIT`.

Posteriormente simular un error y comprobar el efecto de `ROLLBACK`.

## Ejercicio guiado 2 (Profesor)

Simular dos usuarios modificando simultáneamente el stock de un mismo producto.

Analizar:

- posibles conflictos;
- resultado esperado;
- mecanismos de protección.

## Ejercicios de aula

### Bloque A. Diseño de transacciones

#### Ejercicio 1

Crear una transacción para registrar un cliente y su dirección.

#### Ejercicio 2

Registrar un nuevo proveedor junto con los productos que suministra.

#### Ejercicio 3

Actualizar simultáneamente el precio y el stock de varios productos.

#### Ejercicio 4

Eliminar un pedido junto con todas sus líneas de detalle.

---

### Bloque B. COMMIT y ROLLBACK

#### Ejercicio 5

Realizar varias modificaciones y confirmarlas mediante `COMMIT`.

#### Ejercicio 6

Repetir el ejercicio anterior utilizando `ROLLBACK`.

#### Ejercicio 7

Comprobar qué información permanece almacenada tras cada operación.

#### Ejercicio 8

Explicar verbalmente el resultado obtenido.

---

### Bloque C. SAVEPOINT

#### Ejercicio 9

Crear varios puntos de restauración durante una transacción.

#### Ejercicio 10

Volver únicamente al último `SAVEPOINT`.

#### Ejercicio 11

Comparar el resultado con un `ROLLBACK` completo.

---

### Bloque D. Casos empresariales

#### Ejercicio 12

Diseñar la transacción necesaria para registrar una devolución.

#### Ejercicio 13

Diseñar una transacción que permita cancelar un pedido restaurando el inventario.

#### Ejercicio 14

Analizar qué operaciones deberían ejecutarse dentro de una misma transacción y cuáles no.

#### Ejercicio 15

Identificar posibles problemas de concurrencia en un comercio electrónico con cientos de usuarios realizando compras simultáneamente.

## Retos

### Reto 1

Diseña una transacción completa para registrar una venta que incluya validaciones de stock y control de errores.

### Reto 2

Investiga qué ocurriría si el servidor se apagara inmediatamente antes del `COMMIT`.

### Reto 3

Analiza qué propiedades ACID intervienen en cada uno de los ejercicios realizados.

## Trabajo autónomo

1. Implementar todas las transacciones propuestas.
2. Simular errores durante la ejecución.
3. Comprobar el estado de la base de datos tras cada prueba.
4. Documentar los resultados obtenidos.

## Lista de comprobación

- ¿He identificado correctamente las operaciones críticas?
- ¿Comprendo cuándo utilizar `ROLLBACK`?
- ¿Sé emplear `SAVEPOINT`?
- ¿He comprobado el comportamiento ante errores?
- ¿Puedo explicar cómo garantizan las transacciones la integridad de la información?

## Conclusiones

Las transacciones representan uno de los pilares fundamentales de cualquier sistema gestor de bases de datos. Gracias a ellas es posible garantizar que operaciones complejas se ejecuten de forma segura incluso cuando intervienen múltiples usuarios y se producen errores durante la ejecución. En aplicaciones empresariales como TechShop constituyen un mecanismo imprescindible para preservar la consistencia y fiabilidad de la información.

