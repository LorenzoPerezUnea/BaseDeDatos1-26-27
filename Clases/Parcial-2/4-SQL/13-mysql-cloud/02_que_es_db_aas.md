# ¿Qué es DBaaS?

## Introducción

En el capítulo anterior vimos que cada vez más organizaciones deciden trasladar sus bases de datos desde servidores propios hacia plataformas cloud.

Sin embargo, todavía no hemos respondido una pregunta fundamental:

> **¿Qué es exactamente el servicio que estamos contratando?**

Cuando una empresa utiliza Amazon RDS, Google Cloud SQL, Azure Database for MySQL u otros servicios similares, realmente está utilizando un modelo conocido como **Database as a Service**, normalmente abreviado como **DBaaS**.

Este modelo representa una evolución respecto a la forma tradicional de administrar bases de datos y constituye uno de los pilares del desarrollo moderno de aplicaciones.

## Del software al servicio

Durante muchos años, instalar una base de datos implicaba realizar numerosas tareas:

- Comprar un servidor.
- Instalar un sistema operativo.
- Instalar MySQL.
- Configurar usuarios.
- Ajustar parámetros.
- Configurar copias de seguridad.
- Supervisar el servidor.
- Aplicar actualizaciones.
- Resolver incidencias de hardware.

Todo este trabajo recaía sobre el departamento de sistemas.

Con DBaaS gran parte de estas tareas pasan a ser responsabilidad del proveedor cloud.

La empresa consume la base de datos como un servicio, del mismo modo que consume electricidad o conexión a Internet.

## ¿Qué significa "As a Service"?

El término **As a Service** hace referencia a un modelo en el que un proveedor ofrece una funcionalidad completamente preparada para ser utilizada.

El cliente no necesita construir toda la infraestructura desde cero.

Simplemente solicita el servicio y comienza a utilizarlo.

En el caso de DBaaS:

- El proveedor administra la infraestructura.
- El proveedor mantiene el hardware.
- El proveedor monitoriza la plataforma.
- El proveedor automatiza numerosas tareas de mantenimiento.

Mientras tanto, el cliente se centra principalmente en:

- Diseñar la base de datos.
- Crear tablas.
- Escribir consultas.
- Gestionar usuarios.
- Desarrollar la aplicación.

## Una analogía sencilla

Imaginemos dos formas de obtener electricidad.

### Modelo tradicional

Construimos nuestra propia central eléctrica.

Debemos comprar:

- Generadores.
- Transformadores.
- Cableado.
- Sistemas de refrigeración.

Además, necesitaremos personal especializado para mantener todo funcionando.

### Modelo como servicio

Simplemente contratamos el suministro eléctrico.

Pagamos por el consumo y dejamos que la compañía eléctrica gestione toda la infraestructura.

DBaaS funciona de una forma muy parecida.

La empresa utiliza la base de datos sin tener que administrar toda la infraestructura física que existe detrás.

## ¿Qué administra el proveedor?

Aunque depende del servicio contratado, normalmente el proveedor se ocupa de aspectos como:

- Hardware.
- Almacenamiento.
- Red.
- Sustitución de discos averiados.
- Monitorización básica.
- Actualizaciones del sistema.
- Copias de seguridad automáticas.
- Replicación.
- Alta disponibilidad.

Todo ello reduce enormemente la carga administrativa.

## ¿Qué sigue administrando el cliente?

DBaaS no significa que el proveedor haga absolutamente todo.

La responsabilidad del cliente continúa siendo muy importante.

Entre otras tareas:

- Diseñar correctamente el esquema relacional.
- Crear índices.
- Optimizar consultas.
- Gestionar permisos de usuarios.
- Definir políticas de acceso.
- Desarrollar procedimientos almacenados.
- Garantizar la calidad de los datos.

En otras palabras, el proveedor administra la infraestructura, pero la lógica de negocio sigue siendo responsabilidad de la empresa.

## Ventajas de DBaaS

### Menor complejidad

No es necesario instalar ni configurar servidores desde cero.

### Puesta en marcha rápida

Una nueva instancia de MySQL puede estar disponible en pocos minutos.

### Menor carga administrativa

Muchas tareas repetitivas se automatizan.

### Mayor disponibilidad

Los proveedores suelen ofrecer mecanismos automáticos para reducir interrupciones del servicio.

### Escalabilidad sencilla

En muchos casos es posible aumentar recursos sin migraciones complejas.

## Inconvenientes

DBaaS también presenta algunas limitaciones.

### Menor control

No siempre es posible modificar parámetros internos del sistema operativo o del hardware.

### Dependencia del proveedor

Migrar posteriormente a otra plataforma puede requerir tiempo y planificación.

### Costes variables

El modelo de pago por uso ofrece flexibilidad, pero también puede generar costes elevados si no se supervisa correctamente el consumo.

### Restricciones de configuración

Algunas configuraciones muy específicas disponibles en instalaciones propias pueden no estar permitidas en servicios administrados.

## Ejemplo práctico

La empresa TechShop necesita desplegar una nueva aplicación.

Tiene dos posibilidades.

### Opción A

Comprar:

- Servidores.
- Discos.
- Sistemas de alimentación.
- Equipos de respaldo.

Instalar manualmente:

- Linux.
- MySQL.
- Sistemas de monitorización.
- Copias de seguridad.

### Opción B

Crear una instancia MySQL en un servicio DBaaS.

En pocos minutos dispone de una base de datos funcional con:

- Almacenamiento.
- Copias automáticas.
- Monitorización.
- Alta disponibilidad opcional.

La segunda alternativa permite comenzar el desarrollo mucho antes.

## ¿Cuándo utilizar DBaaS?

DBaaS resulta especialmente adecuado para:

- Aplicaciones web.
- Comercio electrónico.
- APIs.
- Sistemas SaaS.
- Aplicaciones móviles.
- Microservicios.
- Startups.
- Empresas con equipos de administración reducidos.

No obstante, aplicaciones con requisitos muy específicos pueden seguir optando por infraestructuras propias.

## Buenas prácticas

- Comprender qué tareas administra el proveedor y cuáles siguen siendo responsabilidad del cliente.
- Diseñar la base de datos con los mismos criterios de calidad que en una instalación local.
- Supervisar periódicamente el consumo de recursos.
- Mantener una estrategia propia de recuperación ante desastres.
- Revisar periódicamente la configuración de seguridad.

## Conclusiones

DBaaS ha transformado la forma en que las organizaciones despliegan bases de datos. Al delegar la administración de la infraestructura en un proveedor especializado, los equipos pueden concentrarse en desarrollar aplicaciones y gestionar la información, reduciendo significativamente la complejidad operativa sin renunciar a las capacidades de MySQL.

## Ideas clave

- DBaaS significa **Database as a Service**.
- El proveedor administra la infraestructura.
- El cliente sigue siendo responsable del diseño y del contenido de la base de datos.
- La automatización reduce la carga administrativa.
- DBaaS constituye actualmente uno de los modelos más utilizados para desplegar bases de datos relacionales.

