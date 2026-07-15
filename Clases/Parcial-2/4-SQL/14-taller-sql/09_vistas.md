# Vistas

## Introducción

A medida que una base de datos crece, también aumenta el número de consultas utilizadas por los usuarios y por las aplicaciones.

En muchas ocasiones distintas consultas reutilizan exactamente la misma combinación de tablas y filtros.

Copiar continuamente esas consultas provoca:

- duplicación de código;
- mayor dificultad de mantenimiento;
- incremento del riesgo de errores.

Las **vistas** permiten encapsular consultas complejas bajo un nombre sencillo, facilitando su reutilización.

Durante este bloque los estudiantes deberán diseñar un conjunto de vistas que podrían utilizarse diariamente en TechShop.

## Objetivos del bloque

Al finalizar este bloque el estudiante será capaz de:

- Diseñar vistas útiles.
- Simplificar consultas complejas.
- Reutilizar consultas frecuentes.
- Identificar cuándo una vista aporta valor.
- Documentar correctamente las vistas creadas.

## Recomendaciones

Antes de crear una vista pregúntate:

- ¿La consulta será reutilizada?
- ¿Facilita el trabajo de otros desarrolladores?
- ¿Oculta complejidad innecesaria?
- ¿Su nombre describe claramente la información que devuelve?

Una vista no debe convertirse en un sustituto de un buen diseño de la base de datos.

## Ejercicio guiado 1 (Profesor)

Crear una vista denominada `vw_clientes` que muestre:

- identificador;
- nombre completo;
- correo electrónico;
- fecha de registro.

Analizar sus ventajas frente a repetir continuamente la consulta.

## Ejercicio guiado 2 (Profesor)

Crear una vista que muestre todos los pedidos junto con el nombre del cliente.

Posteriormente utilizar la vista para realizar nuevas consultas.

## Ejercicios de aula

### Bloque A. Vistas sencillas

#### Ejercicio 1

Crear una vista con todos los productos.

#### Ejercicio 2

Crear una vista con todos los proveedores.

#### Ejercicio 3

Crear una vista con los empleados y su departamento.

#### Ejercicio 4

Crear una vista con todas las categorías.

#### Ejercicio 5

Crear una vista con todos los clientes activos.

---

### Bloque B. Vistas con JOIN

#### Ejercicio 6

Crear una vista que muestre:

- pedido;
- cliente;
- fecha.

#### Ejercicio 7

Crear una vista con:

- producto;
- categoría.

#### Ejercicio 8

Crear una vista con:

- producto;
- proveedor.

#### Ejercicio 9

Crear una vista con:

- pedido;
- estado del envío.

#### Ejercicio 10

Crear una vista que reúna toda la información principal de una línea de pedido.

---

### Bloque C. Vistas para informes

#### Ejercicio 11

Diseñar una vista con estadísticas de ventas por categoría.

#### Ejercicio 12

Crear una vista con el número de pedidos por cliente.

#### Ejercicio 13

Crear una vista con el valor actual del inventario.

#### Ejercicio 14

Diseñar una vista para la dirección comercial mostrando los productos con menor stock.

---

### Bloque D. Uso de vistas

#### Ejercicio 15

Consultar únicamente los diez primeros registros de una vista.

#### Ejercicio 16

Ordenar una vista por un criterio determinado.

#### Ejercicio 17

Aplicar filtros sobre una vista existente.

#### Ejercicio 18

Utilizar una vista dentro de otra consulta.

#### Ejercicio 19

Comparar una consulta escrita directamente con otra basada en una vista.

## Retos

### Reto 1

Diseña un conjunto de vistas que utilizaría diariamente el departamento comercial.

### Reto 2

Propón una nomenclatura coherente para todas las vistas del proyecto.

### Reto 3

Analiza qué vistas podrían dejar de ser útiles si el modelo creciera significativamente.

## Trabajo autónomo

1. Crear todas las vistas propuestas.
2. Documentar su finalidad.
3. Comprobar que cada una devuelve la información esperada.
4. Identificar consultas repetidas que puedan sustituirse mediante vistas.

## Lista de comprobación

- ¿El nombre de cada vista describe claramente su contenido?
- ¿Las vistas simplifican realmente las consultas?
- ¿Evitan duplicar código SQL?
- ¿He comprobado que funcionan correctamente?
- ¿Podrían reutilizarse en una aplicación real?

## Conclusiones

Las vistas constituyen un excelente mecanismo para encapsular consultas frecuentes, mejorar la organización del código SQL y facilitar el mantenimiento de aplicaciones empresariales. Utilizadas correctamente, aumentan la claridad del sistema sin modificar el modelo físico de la base de datos.

