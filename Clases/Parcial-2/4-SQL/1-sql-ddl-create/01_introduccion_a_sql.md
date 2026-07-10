# Introducción a SQL

## Introducción

Hasta este momento del curso, SQL ha aparecido como el lenguaje utilizado para expresar consultas equivalentes a las operaciones del Álgebra Relacional. Sin embargo, reducir SQL a un simple lenguaje de consulta sería una visión muy incompleta.

En realidad, SQL constituye un lenguaje mucho más amplio. Permite crear bases de datos, definir tablas, establecer restricciones de integridad, insertar registros, modificar información, controlar permisos de usuarios, administrar transacciones e incluso definir procedimientos almacenados y desencadenadores.

En otras palabras, SQL proporciona prácticamente todas las herramientas necesarias para administrar el ciclo de vida completo de una base de datos relacional.

Antes de comenzar a utilizarlo es conveniente comprender cuál es su propósito y por qué se ha convertido en el estándar utilizado por prácticamente todos los sistemas gestores de bases de datos relacionales.

### ¿Qué significa SQL?

Las siglas **SQL** corresponden a ​**Structured Query Language**​, que puede traducirse como ​**Lenguaje Estructurado de Consultas**​.

Aunque el nombre hace referencia a las consultas, el lenguaje evolucionó rápidamente hasta incorporar muchas otras funcionalidades.

Actualmente SQL permite:

* crear bases de datos;
* crear tablas;
* definir restricciones;
* insertar registros;
* modificar datos;
* eliminar información;
* controlar permisos;
* gestionar transacciones;
* crear vistas;
* definir procedimientos almacenados;
* automatizar tareas mediante disparadores.

Por este motivo suele afirmarse que SQL es un ​**lenguaje de definición, manipulación y administración de bases de datos**​, y no únicamente un lenguaje de consulta.

### Un estándar, no un producto

Un aspecto importante que suele generar confusión es distinguir SQL de los sistemas gestores de bases de datos.

SQL no es un programa.

SQL es un lenguaje.

Los programas son los SGBD que implementan ese lenguaje.

Por ejemplo:

| Sistema gestor       | Utiliza SQL |
| ---------------------- | ------------- |
| MySQL                | Sí         |
| MariaDB              | Sí         |
| PostgreSQL           | Sí         |
| Oracle Database      | Sí         |
| Microsoft SQL Server | Sí         |

Todos estos productos utilizan SQL, aunque cada uno incorpora pequeñas extensiones propias.

Esta situación es comparable a los lenguajes de programación.

Un mismo programa escrito en Java puede ejecutarse en distintas máquinas virtuales.

De forma similar, una consulta SQL puede ejecutarse en diferentes sistemas gestores con pequeñas modificaciones.

### SQL y el estándar ANSI

Con el paso de los años SQL fue evolucionando y se convirtió en un estándar internacional.

Organizaciones como ANSI e ISO publican periódicamente nuevas versiones del estándar que incorporan funcionalidades adicionales.

Los fabricantes intentan seguir estas especificaciones para mantener la compatibilidad entre productos.

Sin embargo, ningún sistema gestor implementa absolutamente todo el estándar.

Por ello existen diferencias entre MySQL, PostgreSQL, Oracle o SQL Server.

Durante este curso utilizaremos ​**MySQL**​, procurando emplear siempre que sea posible instrucciones compatibles con el estándar SQL.

### SQL como interfaz entre el usuario y la base de datos

El usuario no manipula directamente los archivos donde se almacena la información.

Toda interacción con la base de datos se realiza mediante SQL.

Cuando escribimos una instrucción como:

```sql
CREATE DATABASE EmpresaTecnologica;
```

o

```sql
SELECT Nombre
FROM Cliente;
```

no estamos modificando archivos directamente.

Estamos enviando una petición al sistema gestor.

Será el SGBD quien interprete la instrucción, compruebe que es válida y realice internamente todas las operaciones necesarias.

Este mecanismo garantiza la integridad de los datos y permite que múltiples usuarios trabajen simultáneamente sobre la misma base de datos.

### Nuestro objetivo durante el resto del curso

Hasta ahora el objetivo consistía en comprender cómo se representan y relacionan los datos.

A partir de esta clase comenzaremos a convertir ese conocimiento en una implementación real.

Cada nueva sentencia SQL que aprendamos se aplicará inmediatamente sobre la base de datos de la empresa comercial desarrollada desde el inicio de la asignatura.

Al finalizar el semestre habremos construido una base de datos completa siguiendo exactamente las mismas prácticas utilizadas en proyectos profesionales.

### Errores frecuentes

Un error muy habitual consiste en pensar que SQL solo sirve para realizar consultas.

Otro error frecuente consiste en confundir SQL con MySQL, creyendo que ambos términos representan la misma tecnología.

También es común pensar que todas las variantes de SQL son idénticas. Aunque comparten un núcleo común, cada sistema gestor incorpora características específicas que conviene conocer.

### Ideas clave

* SQL es mucho más que un lenguaje de consulta.
* SQL es un estándar internacional, no un sistema gestor de bases de datos.
* MySQL es uno de los muchos productos que implementan SQL.
* Toda interacción con una base de datos relacional se realiza mediante instrucciones SQL.
* Durante el resto del curso utilizaremos SQL para construir progresivamente una base de datos profesional basada en el caso práctico.

