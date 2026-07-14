# Alta disponibilidad

## Introducción

Cuando una empresa desarrolla una aplicación para uso interno, una interrupción del servicio durante unos minutos puede ser aceptable.

Sin embargo, existen muchos sistemas donde una caída de la base de datos supone consecuencias importantes:

- Una tienda en línea deja de vender.
- Un banco no puede procesar transferencias.
- Un hospital pierde acceso al historial clínico.
- Una plataforma de streaming deja de servir contenido.
- Un sistema logístico no puede registrar nuevos pedidos.

En estos escenarios, la disponibilidad de la base de datos es un requisito crítico.

Por este motivo, los proveedores cloud ofrecen mecanismos de **alta disponibilidad** (High Availability o HA), cuyo objetivo es minimizar el tiempo durante el cual una base de datos permanece inaccesible.

## ¿Qué significa alta disponibilidad?

Una base de datos presenta alta disponibilidad cuando está diseñada para seguir prestando servicio incluso si alguno de sus componentes falla.

Es importante destacar que **alta disponibilidad no significa disponibilidad absoluta**.

Todo sistema informático puede sufrir interrupciones.

El objetivo consiste en reducir al máximo:

- la frecuencia de los fallos,
- la duración de las interrupciones,
- y el impacto sobre los usuarios.

## El problema de un único servidor

Supongamos que TechShop ejecuta MySQL en un único servidor.

```text
Aplicación

      │

      │

Servidor MySQL
```

Si ese servidor deja de funcionar debido a un fallo de hardware, una avería eléctrica o un problema del sistema operativo, la base de datos deja de estar disponible.

Toda la aplicación queda afectada.

Este tipo de arquitectura presenta un **punto único de fallo** (*Single Point of Failure*).

## Eliminando el punto único de fallo

Una estrategia habitual consiste en mantener una segunda instancia preparada para asumir el servicio.

```text
Aplicación

        │

        │

Servidor principal

        │

 Replicación

        │

Servidor secundario
```

Mientras el servidor principal funciona correctamente, el secundario mantiene una copia sincronizada de los datos.

Si el principal deja de estar disponible, el secundario puede asumir su función.

Este proceso recibe el nombre de **failover**.

## ¿Cómo funciona el failover?

Imaginemos la siguiente situación:

1. La aplicación trabaja normalmente con el servidor principal.
2. Se produce un fallo físico.
3. El sistema detecta automáticamente la incidencia.
4. El servidor secundario pasa a ser el nuevo servidor principal.
5. La aplicación continúa funcionando.

El objetivo es que esta transición resulte lo más rápida y transparente posible.

## Alta disponibilidad en AWS RDS

Amazon RDS ofrece una opción denominada **Multi-AZ**.

En este modo:

- Existe una instancia principal.
- Existe una réplica sincronizada en otra zona de disponibilidad.
- Amazon supervisa continuamente ambas instancias.
- Si detecta un fallo, realiza automáticamente el cambio al servidor secundario.

Todo este proceso requiere muy poca intervención del usuario.

## Alta disponibilidad en Google Cloud SQL

Google Cloud SQL ofrece una funcionalidad muy similar.

La plataforma mantiene una réplica sincronizada preparada para asumir el servicio cuando sea necesario.

Al igual que ocurre en AWS, el objetivo consiste en reducir el tiempo de interrupción y simplificar la recuperación.

## Alta disponibilidad no es una copia de seguridad

Es frecuente confundir ambos conceptos.

Sin embargo, resuelven problemas distintos.

La alta disponibilidad protege frente a:

- Fallos de hardware.
- Averías del servidor.
- Interrupciones de determinados componentes.

Las copias de seguridad permiten recuperar información cuando:

- Un usuario elimina datos accidentalmente.
- Una aplicación introduce información incorrecta.
- Se produce corrupción lógica de la información.
- Es necesario restaurar el estado de la base de datos en un momento anterior.

Ambos mecanismos son complementarios.

## ¿Tiene algún coste?

Sí.

Mantener un segundo servidor preparado para asumir el servicio implica consumir recursos adicionales.

Por ello, las configuraciones con alta disponibilidad suelen tener un coste superior al de una única instancia.

Cada organización debe valorar si ese incremento de coste está justificado por la reducción del riesgo.

## ¿Todas las aplicaciones la necesitan?

No necesariamente.

Un pequeño proyecto académico probablemente no requiera una arquitectura altamente disponible.

En cambio, aplicaciones como:

- comercio electrónico,
- banca,
- sanidad,
- plataformas SaaS,
- administración pública,

normalmente consideran la alta disponibilidad un requisito esencial.

## Caso práctico

TechShop recibe miles de pedidos diarios.

Cada minuto de interrupción supone pérdidas económicas.

La empresa decide activar una configuración de alta disponibilidad.

Aunque el coste mensual aumenta, la probabilidad de una interrupción prolongada disminuye considerablemente.

La decisión resulta rentable porque protege el funcionamiento continuo del negocio.

## Buenas prácticas

- Identificar si la aplicación realmente necesita alta disponibilidad.
- Combinar alta disponibilidad con copias de seguridad.
- Supervisar continuamente el estado de la infraestructura.
- Probar periódicamente los procedimientos de recuperación.
- No asumir que la alta disponibilidad elimina todos los posibles fallos.

## Conclusiones

La alta disponibilidad permite reducir el impacto de determinados fallos de infraestructura mediante mecanismos de redundancia y conmutación automática. Servicios como Amazon RDS y Google Cloud SQL incorporan estas capacidades de forma integrada, facilitando el desarrollo de aplicaciones críticas que requieren un elevado nivel de disponibilidad.

## Ideas clave

- Alta disponibilidad significa minimizar interrupciones del servicio.
- El principal enemigo es el punto único de fallo.
- El failover permite sustituir automáticamente un servidor averiado.
- Alta disponibilidad y copias de seguridad resuelven problemas distintos.
- Las aplicaciones críticas suelen justificar el coste adicional de estas configuraciones.

