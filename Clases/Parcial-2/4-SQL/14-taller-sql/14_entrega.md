# Entrega

## Introducción

El desarrollo de una base de datos no concluye cuando todas las tablas han sido creadas o cuando las consultas devuelven los resultados esperados.

En un entorno profesional, el trabajo finaliza únicamente cuando el proyecto puede entregarse a otro equipo con la confianza de que será comprensible, ejecutable y mantenible.

La entrega constituye la última fase del ciclo de desarrollo y representa la oportunidad de demostrar no solo conocimientos técnicos, sino también organización, documentación y capacidad para presentar una solución profesional.

En este bloque se describen los requisitos que deberá cumplir la entrega final del proyecto TechShop.

## Objetivos

Al finalizar este bloque el estudiante será capaz de:

- Organizar correctamente un proyecto de bases de datos.
- Preparar una entrega profesional.
- Verificar el funcionamiento completo de la solución.
- Revisar la calidad del código SQL.
- Presentar y defender técnicamente el trabajo realizado.

## Estructura recomendada del proyecto

Se recomienda organizar el proyecto utilizando una estructura similar a la siguiente.

```text
TechShop/

│

├── README.md

├── sql/

│   ├── 01_creacion_esquema.sql

│   ├── 02_datos_iniciales.sql

│   ├── 03_consultas.sql

│   ├── 04_vistas.sql

│   ├── 05_procedimientos.sql

│   ├── 06_transacciones.sql

│   └── 07_indices.sql

│

├── documentacion/

│   ├── modelo_relacional.pdf

│   ├── diccionario_datos.pdf

│   ├── memoria_tecnica.pdf

│   └── capturas/

│

└── recursos/

    ├── diagrama_ER.png

    └── otros_archivos
```

La organización puede adaptarse ligeramente, pero deberá mantenerse una estructura clara y coherente.

## Criterios de evaluación

El profesor valorará especialmente los siguientes aspectos.

### Diseño del modelo

- Corrección del modelo relacional.
- Uso adecuado de claves primarias.
- Uso correcto de claves foráneas.
- Nivel de normalización.
- Coherencia general.

### Calidad del código SQL

- Legibilidad.
- Organización.
- Nombres descriptivos.
- Comentarios cuando resulten necesarios.
- Ausencia de código duplicado.

### Consultas

Se valorará:

- corrección de los resultados;
- claridad;
- eficiencia;
- uso apropiado de JOIN;
- uso correcto de funciones de agregación;
- empleo adecuado de subconsultas.

### Objetos de base de datos

Se comprobará:

- funcionamiento de las vistas;
- funcionamiento de los procedimientos;
- utilización correcta de transacciones.

### Optimización

Se evaluará:

- utilización de índices;
- análisis mediante EXPLAIN;
- justificación de las optimizaciones.

### Documentación

La documentación deberá ser:

- completa;
- clara;
- organizada;
- coherente con la implementación.

## Lista de comprobación antes de entregar

Antes de realizar la entrega definitiva revisa cuidadosamente los siguientes puntos.

### Base de datos

- Todas las tablas se crean correctamente.
- No existen errores de sintaxis.
- Todas las claves funcionan.
- No existen referencias inválidas.

### Datos

- La carga inicial funciona sin errores.
- Los datos son coherentes.
- Existen suficientes registros para probar las consultas.

### Consultas

- Todas producen el resultado esperado.
- No contienen errores de sintaxis.
- Están correctamente organizadas.

### Procedimientos

- Compilan correctamente.
- Funcionan con distintos parámetros.
- Gestionan adecuadamente posibles errores.

### Transacciones

- Los COMMIT funcionan correctamente.
- Los ROLLBACK restauran el estado esperado.
- Las pruebas de concurrencia son coherentes.

### Optimización

- Se han revisado las consultas principales.
- Los índices utilizados están justificados.
- EXPLAIN confirma el comportamiento esperado.

### Documentación

- El README está actualizado.
- Existe diccionario de datos.
- El modelo está documentado.
- Se describen todas las decisiones importantes.

## Ejercicio guiado (Profesor)

Realizar una revisión completa del proyecto utilizando la lista de comprobación anterior.

Detectar posibles problemas antes de la entrega.

El profesor mostrará cómo realizar una revisión sistemática similar a la utilizada en equipos profesionales.

## Ejercicios de aula

### Ejercicio 1

Revisar la estructura completa del proyecto.

### Ejercicio 2

Comprobar que todos los scripts pueden ejecutarse desde cero.

### Ejercicio 3

Solicitar a otro compañero que revise el proyecto.

Anotar todas las observaciones recibidas.

### Ejercicio 4

Corregir los problemas detectados durante la revisión.

### Ejercicio 5

Preparar una breve presentación (5-10 minutos) explicando:

- el modelo de datos;
- las principales consultas;
- las decisiones de diseño;
- las optimizaciones realizadas.

### Ejercicio 6

Responder a preguntas técnicas planteadas por el profesor o por otros compañeros.

## Retos

### Reto 1

Reducir al máximo el tiempo necesario para desplegar completamente la base de datos desde cero.

### Reto 2

Preparar el proyecto para que pueda ser utilizado como portfolio profesional en GitHub.

### Reto 3

Proponer tres mejoras que podrían desarrollarse en una segunda versión de TechShop.

## Reflexión final

Durante este taller se ha recorrido el ciclo completo de desarrollo de una base de datos relacional.

Se ha partido de un problema empresarial realista y, paso a paso, se ha construido una solución completa que incluye:

- análisis del problema;
- diseño del modelo;
- implementación del esquema;
- carga de datos;
- consultas SQL;
- vistas;
- procedimientos almacenados;
- transacciones;
- optimización;
- documentación.

Este proceso reproduce, a pequeña escala, el trabajo que realizan diariamente equipos de desarrollo y administración de bases de datos en empresas de cualquier tamaño.

## Competencias adquiridas

Al finalizar el taller el estudiante habrá demostrado que es capaz de:

- Analizar requisitos empresariales.
- Diseñar un modelo relacional coherente.
- Implementar una base de datos completa en MySQL.
- Desarrollar consultas sencillas y avanzadas.
- Optimizar el rendimiento.
- Garantizar la integridad mediante transacciones.
- Documentar correctamente un proyecto técnico.
- Preparar una entrega profesional.

## Conclusión

Este taller pone el broche final al curso de Bases de Datos Relacionales. Más allá de la sintaxis de SQL, el estudiante ha trabajado con un caso práctico que integra análisis, diseño, implementación, validación y documentación, reproduciendo el flujo de trabajo habitual en proyectos reales.

Las competencias desarrolladas servirán como base para abordar con solvencia tecnologías más avanzadas y otros modelos de almacenamiento, especialmente los estudiados en la asignatura de **Bases de Datos NoSQL**, donde muchos de los principios aprendidos seguirán siendo fundamentales aunque cambie la tecnología empleada.

