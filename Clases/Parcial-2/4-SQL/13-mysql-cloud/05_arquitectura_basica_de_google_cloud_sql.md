# Arquitectura básica de Google Cloud SQL

## Introducción

Otro de los grandes proveedores de servicios cloud es **Google Cloud Platform (GCP)**.

Al igual que AWS, ofrece una enorme variedad de servicios relacionados con computación, almacenamiento, inteligencia artificial, análisis de datos y redes.

Para bases de datos relacionales, Google proporciona un servicio administrado denominado **Cloud SQL**.

Su filosofía es muy similar a Amazon RDS: permitir que empresas y desarrolladores utilicen motores de bases de datos ampliamente conocidos sin tener que administrar directamente toda la infraestructura.

Entre los motores soportados se encuentra MySQL, además de PostgreSQL y SQL Server.

## ¿Qué es Google Cloud SQL?

Google Cloud SQL es un servicio **Database as a Service**.

Permite crear instancias administradas de MySQL en pocos minutos.

El usuario continúa utilizando:

- SQL,
- clientes MySQL,
- herramientas de administración,
- aplicaciones existentes.

La principal diferencia radica en que Google administra la infraestructura necesaria para mantener la base de datos en funcionamiento.

## Componentes principales

Desde una perspectiva simplificada podemos identificar varios elementos.

### Aplicaciones cliente

Pueden conectarse:

- aplicaciones web,
- APIs,
- programas de escritorio,
- herramientas administrativas,
- servicios desplegados en Google Cloud.

Todas ellas utilizan el protocolo habitual de MySQL.

### Instancia Cloud SQL

La instancia contiene el motor MySQL.

Durante su creación el usuario selecciona:

- versión,
- memoria,
- procesadores,
- almacenamiento,
- ubicación geográfica,
- opciones de disponibilidad.

Google configura automáticamente el resto de la infraestructura.

### Almacenamiento administrado

Los datos se almacenan sobre la infraestructura distribuida de Google.

No es necesario gestionar discos físicos ni sistemas RAID manualmente.

### Infraestructura de red

Google proporciona mecanismos para controlar qué aplicaciones pueden acceder a la base de datos mediante redes privadas, direcciones autorizadas y otras políticas de seguridad.

## Arquitectura simplificada

```text
Aplicación

        │

        │

 Google Cloud

        │

+------------------------+
|     Cloud SQL          |
|------------------------|
|       MySQL 8          |
|------------------------|
| Almacenamiento Cloud   |
+------------------------+

        │

Copias automáticas
Monitorización
Alta disponibilidad
```

Este esquema resume los componentes esenciales desde el punto de vista del desarrollador.

## Creación de una instancia

El procedimiento habitual consiste en:

1. Seleccionar MySQL.
2. Elegir la versión.
3. Configurar CPU y memoria.
4. Definir almacenamiento.
5. Configurar autenticación.
6. Crear la instancia.

Tras unos minutos Google proporciona la información necesaria para establecer la conexión desde la aplicación.

## Administración automática

Google automatiza numerosas tareas relacionadas con la infraestructura.

Entre ellas:

- mantenimiento del hardware,
- supervisión de la plataforma,
- actualizaciones controladas,
- almacenamiento,
- recuperación ante determinados fallos.

Esto reduce significativamente la carga de administración.

## Responsabilidades del usuario

Al igual que sucede en AWS, el desarrollador continúa siendo responsable de:

- diseño del esquema,
- consultas SQL,
- índices,
- procedimientos almacenados,
- rendimiento,
- seguridad lógica,
- usuarios y permisos.

La automatización de la infraestructura no elimina la necesidad de diseñar correctamente la base de datos.

## Integración con Google Cloud

Cloud SQL puede integrarse fácilmente con otros servicios del ecosistema Google.

Por ejemplo:

- aplicaciones desplegadas en Compute Engine,
- servicios serverless,
- Kubernetes,
- herramientas de análisis de datos,
- sistemas de monitorización.

Esta integración facilita la construcción de aplicaciones distribuidas.

## Comparación con Amazon RDS

Desde el punto de vista del desarrollador ambos servicios ofrecen una experiencia muy similar.

En ambos casos:

- se utiliza MySQL,
- las consultas SQL no cambian,
- existen copias automáticas,
- la infraestructura está administrada,
- es posible aumentar recursos con relativa facilidad.

Las diferencias suelen encontrarse en aspectos relacionados con:

- precios,
- integración con otros servicios cloud,
- herramientas de administración,
- preferencias tecnológicas de cada organización.

## Caso práctico

TechShop desarrolla una nueva plataforma basada completamente en Google Cloud.

La empresa despliega:

- la aplicación web,
- los servicios de autenticación,
- el almacenamiento de archivos,
- y la base de datos mediante Cloud SQL.

Desde el punto de vista del equipo de desarrollo, el trabajo con MySQL continúa siendo prácticamente idéntico al realizado durante todo el curso.

## Buenas prácticas

- Seleccionar correctamente la región donde se desplegará la instancia.
- Configurar redes privadas cuando sea posible.
- Supervisar periódicamente el uso de recursos.
- Mantener políticas adecuadas de control de acceso.
- Revisar las configuraciones de copia de seguridad y recuperación.

## Conclusiones

Google Cloud SQL ofrece una solución administrada para ejecutar MySQL en la nube reduciendo significativamente la complejidad de administrar la infraestructura. Comparte gran parte de la filosofía de Amazon RDS y constituye una opción ampliamente utilizada para desplegar aplicaciones modernas sobre Google Cloud Platform.

## Ideas clave

- Google Cloud SQL es un servicio DBaaS.
- Permite utilizar MySQL sin administrar directamente la infraestructura.
- El proveedor mantiene el hardware y la plataforma.
- El cliente continúa siendo responsable del diseño y del contenido de la base de datos.
- La integración con otros servicios de Google Cloud facilita el desarrollo de aplicaciones distribuidas.

