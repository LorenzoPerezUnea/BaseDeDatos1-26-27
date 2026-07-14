# MySQL On-Premise vs Cloud

## Introducción

Una vez comprendido qué es **Database as a Service (DBaaS)**, surge una pregunta inevitable:

> **¿Qué diferencias existen entre instalar MySQL en un servidor propio y utilizar un servicio administrado en la nube?**

A primera vista ambas opciones parecen equivalentes.

En ambos casos:

- utilizamos MySQL,
- escribimos consultas SQL,
- creamos tablas,
- ejecutamos procedimientos almacenados,
- gestionamos transacciones.

Sin embargo, la forma en que se administra la infraestructura cambia de manera considerable.

Comprender estas diferencias permite elegir la solución más adecuada para cada proyecto.

## Modelo On-Premise

En una instalación **On-Premise**, la organización es propietaria de toda la infraestructura.

Esto incluye:

- Servidores físicos.
- Sistemas de almacenamiento.
- Redes.
- Alimentación eléctrica.
- Sistemas de refrigeración.
- Copias de seguridad.
- Seguridad física.

Además, el equipo técnico debe instalar y mantener:

- Sistema operativo.
- MySQL.
- Actualizaciones.
- Monitorización.
- Herramientas de administración.

El control es prácticamente absoluto, pero también lo es la responsabilidad.

## Modelo Cloud

En un entorno cloud la empresa sigue utilizando MySQL, pero la infraestructura pertenece al proveedor.

El cliente normalmente administra aspectos relacionados con:

- Bases de datos.
- Usuarios.
- Consultas.
- Seguridad lógica.
- Rendimiento de las aplicaciones.

Mientras tanto, el proveedor se ocupa de tareas como:

- Hardware.
- Almacenamiento.
- Red.
- Sustitución de componentes averiados.
- Supervisión básica.
- Disponibilidad de la plataforma.

Esto reduce considerablemente el trabajo operativo.

## Comparación general

| Aspecto | On-Premise | Cloud |
|---------|------------|--------|
| Hardware | Propio | Administrado por el proveedor |
| Instalación | Manual | Automatizada |
| Actualizaciones | Responsabilidad de la empresa | Parcial o totalmente automatizadas |
| Escalabilidad | Requiere ampliar infraestructura | Generalmente rápida |
| Copias de seguridad | Configuración propia | Automatizables |
| Alta disponibilidad | Debe diseñarse internamente | Disponible como servicio |
| Inversión inicial | Elevada | Muy reducida |
| Pago | Compra de infraestructura | Pago por uso |

## Tiempo de despliegue

Imaginemos que TechShop necesita una nueva base de datos.

### Instalación local

Es necesario:

1. Comprar el servidor.
2. Instalar el hardware.
3. Configurar la red.
4. Instalar Linux.
5. Instalar MySQL.
6. Configurar seguridad.
7. Configurar copias.
8. Realizar pruebas.

Este proceso puede durar desde varios días hasta semanas.

### Instalación cloud

Normalmente basta con:

1. Elegir la versión de MySQL.
2. Seleccionar memoria y almacenamiento.
3. Configurar usuarios.
4. Esperar unos minutos.

La diferencia de tiempo es evidente.

## Escalabilidad

Supongamos que la base de datos duplica su tamaño.

### On-Premise

Puede ser necesario:

- Comprar más memoria.
- Añadir discos.
- Migrar datos.
- Sustituir servidores.

### Cloud

En muchos casos basta con modificar la configuración de la instancia y permitir que el proveedor realice la ampliación.

No siempre será instantáneo, pero suele requerir mucho menos trabajo.

## Costes

El modelo económico también cambia.

### On-Premise

La empresa realiza una inversión inicial importante.

Posteriormente aparecen costes relacionados con:

- Electricidad.
- Mantenimiento.
- Renovación de hardware.
- Personal técnico.

### Cloud

Generalmente no existe una gran inversión inicial.

El coste depende del consumo:

- Horas de ejecución.
- Almacenamiento utilizado.
- Tráfico de red.
- Copias de seguridad.
- Recursos contratados.

Este modelo ofrece mayor flexibilidad, aunque requiere controlar cuidadosamente el gasto.

## Seguridad

En ambos modelos la seguridad sigue siendo fundamental.

La diferencia principal es el reparto de responsabilidades.

En instalaciones propias la empresa protege tanto la infraestructura como los datos.

En servicios cloud el proveedor protege la infraestructura física, mientras que el cliente continúa siendo responsable de:

- Usuarios.
- Contraseñas.
- Permisos.
- Accesos.
- Cifrado cuando corresponda.
- Diseño seguro de la aplicación.

Este reparto suele denominarse **modelo de responsabilidad compartida**.

## ¿Cuál es mejor?

No existe una respuesta universal.

Una pequeña startup probablemente obtenga grandes ventajas utilizando servicios cloud.

Una organización con requisitos regulatorios muy estrictos puede preferir mantener determinadas bases de datos en sus propias instalaciones.

En muchos casos incluso se emplean arquitecturas híbridas donde conviven ambos modelos.

## Buenas prácticas

- Analizar las necesidades reales antes de elegir una arquitectura.
- Considerar el crecimiento previsto de la aplicación.
- Evaluar los costes a largo plazo.
- Tener en cuenta los requisitos legales sobre los datos.
- Diseñar pensando en la disponibilidad y la seguridad.

## Conclusiones

MySQL puede ejecutarse tanto en servidores propios como en plataformas cloud administradas. Ambos modelos son plenamente válidos y cada uno presenta ventajas e inconvenientes. La decisión depende del contexto técnico, económico y organizativo de cada proyecto, por lo que resulta imprescindible analizar cuidadosamente los requisitos antes de seleccionar una solución.

## Ideas clave

- On-Premise proporciona mayor control, pero también mayor responsabilidad.
- Cloud simplifica la administración de la infraestructura.
- La escalabilidad suele ser más sencilla en la nube.
- Los modelos de costes son diferentes.
- La elección debe basarse en las necesidades reales del proyecto y no en tendencias tecnológicas.

