# Casos reales de empresas

## Introducción

A lo largo del curso hemos trabajado con la empresa ficticia **TechShop**, que nos ha permitido estudiar de forma progresiva el diseño, desarrollo y optimización de una base de datos relacional.

Sin embargo, las tecnologías estudiadas no pertenecen únicamente al ámbito académico.

Miles de organizaciones de todo el mundo utilizan diariamente MySQL y servicios de bases de datos administradas para gestionar aplicaciones críticas.

En este capítulo analizaremos distintos escenarios reales donde este tipo de soluciones resultan especialmente adecuadas.

No se pretende estudiar la arquitectura exacta de cada empresa, ya que esta suele evolucionar continuamente y muchos detalles no son públicos, sino comprender **qué tipo de problemas resuelven las bases de datos cloud**.

## Comercio electrónico

Las plataformas de comercio electrónico necesitan almacenar información como:

- clientes,
- productos,
- pedidos,
- pagos,
- envíos,
- inventario.

Durante campañas especiales, como rebajas o promociones, el número de consultas puede multiplicarse en pocas horas.

Utilizar un servicio administrado facilita aumentar recursos cuando la demanda crece y reducirlos posteriormente si la carga disminuye.

Además, las copias automáticas y la alta disponibilidad reducen el riesgo de interrupciones del negocio.

## Plataformas educativas

Universidades, academias y plataformas de formación almacenan:

- estudiantes,
- cursos,
- matrículas,
- evaluaciones,
- materiales docentes.

En determinadas épocas del año, como el inicio del curso o los periodos de matrícula, la actividad aumenta considerablemente.

Los servicios cloud permiten adaptar la infraestructura a estas variaciones sin necesidad de adquirir servidores permanentes para soportar únicamente los momentos de mayor carga.

## Aplicaciones SaaS

Muchas empresas desarrollan aplicaciones ofrecidas como servicio (*Software as a Service*).

Algunos ejemplos son:

- gestores de proyectos,
- herramientas de facturación,
- plataformas CRM,
- sistemas ERP,
- aplicaciones de recursos humanos.

En este tipo de soluciones la disponibilidad resulta fundamental, ya que los clientes esperan poder acceder al servicio en cualquier momento.

Las bases de datos administradas simplifican la gestión de este tipo de aplicaciones.

## Empresas multinacionales

Una organización con sedes en distintos países puede necesitar que sus aplicaciones estén disponibles para usuarios distribuidos geográficamente.

Los proveedores cloud disponen de centros de datos en numerosas regiones del mundo.

Esto permite desplegar la infraestructura cerca de los usuarios, reduciendo la latencia y mejorando la experiencia de uso.

## Startups

Las startups suelen enfrentarse a una situación particular.

Durante los primeros meses desconocen cuál será el crecimiento de su producto.

Comprar una infraestructura muy potente puede resultar innecesario y consumir una parte importante del presupuesto.

Los servicios DBaaS permiten comenzar con recursos modestos y ampliarlos progresivamente conforme aumenta el número de clientes.

Este modelo reduce el riesgo financiero.

## Grandes organizaciones

Las grandes empresas también utilizan servicios cloud, aunque en muchos casos combinan diferentes estrategias.

Es habitual encontrar arquitecturas híbridas donde conviven:

- servidores propios,
- servicios cloud,
- centros de datos distribuidos,
- aplicaciones heredadas.

La elección depende de factores técnicos, económicos y regulatorios.

## El caso de TechShop

Si retomamos el ejemplo desarrollado durante todo el curso, podemos observar cómo la evolución de la empresa justifica la migración hacia una infraestructura cloud.

### Primera etapa

La empresa comienza con una pequeña tienda en línea.

Un único servidor MySQL resulta suficiente.

### Segunda etapa

El número de clientes aumenta.

Se incorporan nuevas funcionalidades.

Comienzan a utilizarse índices, procedimientos almacenados y consultas optimizadas.

### Tercera etapa

La empresa vende internacionalmente.

La disponibilidad pasa a ser un requisito fundamental.

Las copias de seguridad deben automatizarse.

El crecimiento del volumen de datos obliga a ampliar recursos.

En este momento un servicio DBaaS resulta especialmente adecuado.

## ¿Significa esto que todas las empresas deben utilizar la nube?

No.

Existen organizaciones que, por motivos legales, económicos o técnicos, continúan utilizando infraestructuras propias.

Lo importante no es seguir una tendencia tecnológica, sino seleccionar la arquitectura que mejor responda a las necesidades del proyecto.

## Buenas prácticas

- Analizar el contexto concreto de cada organización.
- Evitar adoptar tecnologías únicamente por su popularidad.
- Considerar tanto aspectos técnicos como económicos.
- Planificar el crecimiento desde las primeras fases del proyecto.
- Revisar periódicamente si la arquitectura sigue siendo adecuada.

## Conclusiones

Las bases de datos cloud se utilizan actualmente en una enorme variedad de sectores y organizaciones. Desde pequeñas startups hasta grandes multinacionales, los servicios administrados permiten simplificar la administración de infraestructura y adaptarse con mayor facilidad al crecimiento de las aplicaciones. No obstante, la elección entre nube y servidores propios siempre debe responder a las necesidades reales del negocio.

## Ideas clave

- Las bases de datos cloud están presentes en numerosos sectores.
- El comercio electrónico y las aplicaciones SaaS constituyen algunos de los casos de uso más habituales.
- Las startups se benefician especialmente del modelo de pago por uso.
- Las grandes organizaciones suelen combinar distintas arquitecturas.
- No existe una solución universal válida para todos los proyectos.

