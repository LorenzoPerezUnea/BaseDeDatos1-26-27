# Presentación del caso

## Introducción

En el desarrollo profesional de software es muy poco habitual comenzar un proyecto escribiendo directamente sentencias SQL.

Antes de crear una sola tabla es necesario comprender el negocio para el que se está desarrollando la aplicación.

Un mismo problema puede resolverse mediante múltiples diseños diferentes, pero únicamente algunos de ellos serán fáciles de mantener, eficientes y capaces de evolucionar con el tiempo.

Por ello, este taller comienza exactamente igual que comenzaría un proyecto real: estudiando el problema que plantea el cliente.

## La empresa

La empresa para la que vamos a trabajar se denomina **TechShop**.

TechShop nació hace varios años como una pequeña tienda física especializada en componentes informáticos.

Con el paso del tiempo amplió su actividad incorporando una tienda online.

Actualmente vende productos tecnológicos en todo el territorio nacional.

Su crecimiento ha provocado que el sistema de gestión utilizado hasta ahora resulte insuficiente.

La empresa desea desarrollar una nueva plataforma basada completamente en MySQL.

Nuestro equipo será responsable del diseño e implementación de la base de datos.

## Situación actual

Tras varias reuniones con los responsables de la empresa se obtiene la siguiente información.

La empresa dispone de:

- departamentos administrativos;
- empleados;
- proveedores nacionales e internacionales;
- un catálogo de miles de productos;
- categorías organizadas jerárquicamente;
- clientes registrados;
- pedidos realizados por Internet;
- líneas de detalle para cada pedido;
- pagos;
- control de inventario;
- historial de compras.

Actualmente muchos de estos datos se almacenan mediante hojas de cálculo independientes.

Esto provoca:

- información duplicada;
- errores frecuentes;
- dificultad para generar informes;
- problemas de integridad;
- pérdida de tiempo.

El objetivo del proyecto consiste en unificar toda esta información en una única base de datos relacional.

## Objetivos del proyecto

La nueva base de datos deberá permitir:

- registrar nuevos clientes;
- almacenar información de productos;
- organizar categorías;
- controlar proveedores;
- gestionar pedidos;
- registrar el detalle de cada pedido;
- conocer el inventario disponible;
- realizar consultas comerciales;
- generar estadísticas;
- mantener la integridad de la información.

## Restricciones

El cliente establece varias condiciones importantes.

La solución deberá:

- utilizar MySQL 8;
- seguir el modelo relacional;
- evitar información duplicada;
- garantizar la integridad mediante claves;
- ser fácilmente ampliable;
- estar correctamente documentada.

## Nuestra función

Durante este taller asumiremos el papel de un equipo de ingeniería.

Cada decisión deberá justificarse técnicamente.

No basta con que la base de datos funcione.

También deberá ser:

- mantenible;
- escalable;
- comprensible;
- eficiente.

## Ejercicio guiado 1 (Profesor)

Lee cuidadosamente la descripción de la empresa.

Identifica todas las entidades que aparecen explícitamente en el enunciado.

Posteriormente clasifícalas según pertenezcan a:

- personas;
- organizaciones;
- objetos;
- procesos.

El profesor resolverá este ejercicio mostrando una posible estrategia de análisis.

## Ejercicio guiado 2 (Profesor)

A partir de las entidades identificadas anteriormente, realiza una primera propuesta de relaciones entre ellas.

No es necesario definir todavía atributos ni claves.

Únicamente interesa comprender cómo interactúan los distintos elementos del negocio.

## Ejercicios de aula

### Ejercicio 1

Indica cinco problemas que podrían aparecer si TechShop continuara almacenando la información mediante hojas de cálculo independientes.

### Ejercicio 2

¿Qué ventajas ofrece una base de datos relacional frente a esa solución?

Justifica cada respuesta.

### Ejercicio 3

Clasifica las siguientes operaciones según afecten principalmente a lectura o escritura.

- Registrar un cliente.
- Consultar pedidos.
- Modificar un precio.
- Eliminar un proveedor.
- Obtener el listado de productos.

### Ejercicio 4

Enumera toda la información que debería almacenarse sobre un cliente.

No pienses todavía en tipos de datos.

Simplemente identifica la información relevante.

### Ejercicio 5

Haz lo mismo para un producto.

### Ejercicio 6

Haz lo mismo para un pedido.

## Retos

### Reto 1

¿Qué nuevas funcionalidades podrían incorporarse en el futuro sin necesidad de modificar completamente el modelo de datos?

### Reto 2

Propón al menos cinco informes que probablemente solicitará la dirección de TechShop.

## Trabajo autónomo

1. Describe el funcionamiento completo de la empresa utilizando un máximo de dos páginas.
2. Identifica todas las entidades que consideres necesarias.
3. Propón nuevas entidades que no aparezcan explícitamente en el enunciado pero que podrían resultar útiles.
4. Justifica cada propuesta.

## Lista de comprobación

Antes de continuar con el siguiente bloque deberías ser capaz de responder afirmativamente a todas las preguntas siguientes.

- ¿Comprendo el funcionamiento general de la empresa?
- ¿He identificado las entidades principales?
- ¿Entiendo qué información necesita almacenar el sistema?
- ¿Soy capaz de explicar el problema sin consultar el enunciado?
- ¿Tengo una primera idea de cómo podría diseñarse la base de datos?

## Conclusiones

Antes de diseñar una base de datos resulta imprescindible comprender el negocio para el que va a desarrollarse. Un análisis incompleto conduce casi siempre a modelos incorrectos que posteriormente resultan difíciles y costosos de modificar.

En el siguiente bloque comenzaremos a transformar toda esta información en un modelo de datos estructurado.

