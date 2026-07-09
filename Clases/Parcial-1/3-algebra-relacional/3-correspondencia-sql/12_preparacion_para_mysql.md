# Preparación para MySQL

## Introducción

Con esta clase concluye el estudio del Álgebra Relacional como lenguaje formal de consulta. A partir de la siguiente unidad comenzaremos a trabajar directamente con MySQL, utilizando SQL como herramienta principal para crear, consultar y administrar bases de datos relacionales.

Es importante comprender que este cambio no supone abandonar el Álgebra Relacional. Todo lo contrario. Los conceptos estudiados hasta ahora seguirán presentes durante el resto del curso y constituirán la base sobre la que se apoyará cada nueva sentencia SQL.

De hecho, muchos estudiantes descubren que aprender SQL resulta mucho más sencillo cuando ya comprenden la lógica del Álgebra Relacional. En lugar de memorizar cláusulas aisladas, pueden reconocer que cada una representa una operación cuyo significado ya conocen.

### Del modelo lógico al lenguaje de implementación

Hasta ahora hemos trabajado principalmente en el nivel lógico del Modelo Relacional.

Hemos aprendido a responder preguntas como:

* ¿Cómo se representa la información?
* ¿Qué operaciones pueden realizarse sobre las relaciones?
* ¿Cómo se combinan varias tablas?
* ¿Cómo se construyen consultas complejas?

A partir de la siguiente clase comenzaremos a responder preguntas diferentes:

* ¿Cómo se crea una base de datos en MySQL?
* ¿Cómo se definen tablas reales?
* ¿Cómo se insertan registros?
* ¿Cómo se ejecutan consultas SQL?
* ¿Cómo administra un SGBD la información almacenada?

Puede parecer un cambio importante, pero en realidad es una evolución natural del curso.

El razonamiento seguirá siendo el mismo; únicamente cambiaremos el lenguaje utilizado para expresarlo.

### Lo que ya sabemos

Antes de comenzar con MySQL, el estudiante dispone ya de una base sólida.

Conoce:

* el Modelo Relacional;
* las relaciones, atributos y tuplas;
* las claves primarias y foráneas;
* las restricciones de integridad;
* el Álgebra Relacional;
* las operaciones fundamentales de consulta;
* la correspondencia entre el Álgebra Relacional y SQL.

Esto significa que, cuando aparezca una sentencia como:

```sql
SELECT Nombre
FROM Cliente
WHERE Ciudad='Santander';
```

ya no será una simple combinación de palabras reservadas. El estudiante sabrá que representa una proyección aplicada sobre el resultado de una selección, exactamente igual que en el Álgebra Relacional.

Esta forma de entender SQL proporciona una ventaja muy importante frente al aprendizaje puramente memorístico.

### Qué aprenderemos en el bloque de MySQL

El siguiente bloque del curso estará centrado en la práctica.

Entre otros temas se estudiarán:

* instalación y configuración de MySQL;
* creación de bases de datos;
* definición de tablas;
* tipos de datos;
* claves y restricciones;
* inserción, modificación y eliminación de registros;
* consultas SQL cada vez más complejas;
* funciones, agregaciones y ordenaciones;
* subconsultas y vistas.

Todos estos contenidos utilizarán el mismo caso práctico de la empresa comercial, que continuará creciendo a medida que avance la asignatura.

### Un cambio de perspectiva

Hasta ahora el objetivo era comprender cómo razona una base de datos relacional.

A partir de la siguiente unidad el objetivo será aprender a utilizar un sistema gestor real aplicando ese razonamiento.

El conocimiento adquirido durante las últimas semanas permitirá interpretar cada sentencia SQL desde un punto de vista lógico y no únicamente sintáctico.

Esta forma de trabajar facilitará enormemente el aprendizaje de consultas complejas, optimización y diseño físico, temas que aparecerán en la segunda mitad del curso.

### Ideas clave

* El estudio del Álgebra Relacional concluye, pero sus conceptos seguirán presentes durante todo el curso.
* SQL es la implementación práctica de los principios estudiados hasta ahora.
* Comprender el razonamiento lógico facilita enormemente el aprendizaje de MySQL.
* El siguiente bloque será eminentemente práctico, pero mantendrá la continuidad del caso de estudio.
* El objetivo ya no será aprender nuevas ideas, sino aplicar correctamente las que ya se conocen mediante un sistema gestor de bases de datos real.

