# Arquitectura básica de AWS RDS

## Introducción

Hasta este momento hemos hablado de la nube de una forma general, pero existen numerosos proveedores que ofrecen servicios para alojar bases de datos.

Uno de los más utilizados a nivel mundial es **Amazon Web Services (AWS)**, la plataforma cloud desarrollada por Amazon.

Dentro de AWS existen cientos de servicios diferentes: almacenamiento, redes, inteligencia artificial, análisis de datos, contenedores, monitorización y mucho más.

Entre todos ellos destaca **Amazon Relational Database Service (Amazon RDS)**, un servicio diseñado para facilitar el despliegue y la administración de bases de datos relacionales.

Su objetivo principal es permitir que las empresas utilicen motores como MySQL sin tener que preocuparse por gran parte de la infraestructura necesaria para mantenerlos en funcionamiento.

## ¿Qué es Amazon RDS?

Amazon RDS es un servicio **DBaaS** (Database as a Service).

En lugar de instalar MySQL manualmente sobre un servidor virtual, el usuario solicita una nueva instancia de base de datos y AWS realiza automáticamente gran parte del trabajo necesario para ponerla en funcionamiento.

El desarrollador continúa utilizando MySQL prácticamente igual que en una instalación tradicional:

- crea bases de datos,
- define tablas,
- ejecuta consultas SQL,
- configura usuarios,
- desarrolla procedimientos almacenados.

Sin embargo, muchas tareas administrativas quedan automatizadas.

## Componentes principales

Aunque la infraestructura real de Amazon es extremadamente compleja, desde un punto de vista conceptual podemos simplificarla en varios componentes.

### Cliente

Puede tratarse de:

- una aplicación web,
- una API,
- un programa de escritorio,
- una aplicación móvil,
- un administrador como MySQL Workbench.

Todos ellos establecen una conexión con la base de datos utilizando el protocolo habitual de MySQL.

### Instancia RDS

Es el servidor donde realmente se ejecuta MySQL.

Cuando creamos una instancia debemos seleccionar aspectos como:

- versión de MySQL,
- memoria RAM,
- número de procesadores virtuales,
- capacidad de almacenamiento,
- región geográfica,
- configuración de red.

AWS crea automáticamente toda la infraestructura necesaria.

### Almacenamiento

La información se almacena sobre sistemas distribuidos administrados por Amazon.

El usuario no necesita instalar discos ni configurar volúmenes de almacenamiento.

Simplemente solicita una determinada capacidad y AWS se encarga de administrarla.

### Red

La comunicación entre aplicaciones y la base de datos se realiza mediante la infraestructura de red de AWS.

Es posible limitar qué equipos pueden conectarse utilizando reglas de seguridad específicas.

## Arquitectura simplificada

```text
Aplicación
      │
      │
Internet / Red privada
      │
      │
+----------------------+
|      Amazon RDS      |
|----------------------|
|      MySQL 8         |
|----------------------|
| Almacenamiento Cloud |
+----------------------+
      │
      │
 Copias de seguridad
 Monitorización
 Alta disponibilidad
```

En realidad la arquitectura interna es mucho más compleja, pero este esquema representa correctamente los elementos principales.

## Creación de una instancia

El proceso habitual consiste en:

1. Elegir el motor de base de datos.
2. Seleccionar MySQL.
3. Elegir la versión.
4. Configurar memoria y CPU.
5. Definir almacenamiento.
6. Configurar autenticación.
7. Crear la instancia.

Tras unos minutos AWS proporciona un punto de conexión (endpoint) similar a:

```text
techshop-db.abcdefgh.us-east-1.rds.amazonaws.com
```

Las aplicaciones utilizarán dicho endpoint para conectarse.

## ¿Qué administra AWS?

Amazon se encarga de numerosas tareas relacionadas con la infraestructura.

Entre ellas:

- mantenimiento del hardware,
- sustitución de discos averiados,
- monitorización básica,
- aplicación de determinados parches,
- almacenamiento,
- disponibilidad de la plataforma.

Esto reduce considerablemente el trabajo operativo.

## ¿Qué administra el cliente?

El usuario continúa siendo responsable de aspectos como:

- diseño del modelo relacional,
- creación de tablas,
- índices,
- consultas SQL,
- permisos de usuarios,
- rendimiento de la aplicación,
- calidad de los datos.

AWS administra la infraestructura, pero no el contenido de la base de datos.

## Escalabilidad

Una de las principales ventajas de Amazon RDS consiste en la posibilidad de aumentar recursos con relativa facilidad.

Por ejemplo:

- más memoria,
- mayor capacidad de almacenamiento,
- procesadores más potentes.

Este proceso suele requerir mucha menos intervención que ampliar un servidor físico.

## Integración con otros servicios

Amazon RDS puede trabajar junto con otros servicios del ecosistema AWS.

Por ejemplo:

- aplicaciones desplegadas en servidores virtuales,
- funciones serverless,
- almacenamiento de archivos,
- sistemas de monitorización,
- herramientas de análisis de datos.

Esta integración constituye uno de sus principales atractivos para proyectos de gran tamaño.

## Caso práctico

TechShop decide trasladar su aplicación a AWS.

La empresa crea una instancia MySQL mediante Amazon RDS.

La aplicación web continúa utilizando exactamente las mismas consultas SQL desarrolladas durante este curso.

Sin embargo, ya no necesita administrar directamente:

- discos,
- hardware,
- alimentación eléctrica,
- sustitución de componentes.

El equipo puede concentrarse en desarrollar nuevas funcionalidades.

## Buenas prácticas

- Seleccionar la región más cercana a los usuarios.
- Configurar correctamente las reglas de acceso.
- Supervisar el consumo de recursos.
- Revisar periódicamente las copias de seguridad.
- No asumir que el proveedor sustituye las buenas prácticas de diseño de bases de datos.

## Conclusiones

Amazon RDS simplifica enormemente el despliegue y la administración de MySQL al automatizar numerosas tareas relacionadas con la infraestructura. El desarrollador continúa utilizando SQL y diseñando la base de datos de la misma forma que en una instalación tradicional, pero delega gran parte del mantenimiento operativo en AWS.

## Ideas clave

- Amazon RDS es un servicio DBaaS.
- Automatiza gran parte de la administración de infraestructura.
- El cliente sigue siendo responsable del diseño de la base de datos.
- La escalabilidad y la integración con otros servicios constituyen algunas de sus principales ventajas.
- MySQL se utiliza prácticamente igual que en una instalación local.

