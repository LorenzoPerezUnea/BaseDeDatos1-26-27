# Escalabilidad vertical y horizontal

## Introducción

Uno de los mayores desafíos de cualquier sistema de información consiste en responder a una pregunta aparentemente sencilla:

> **¿Qué ocurre cuando la aplicación comienza a recibir muchos más usuarios de los previstos?**

Durante las primeras fases de un proyecto, una única instancia de MySQL suele ser suficiente para atender todas las consultas.

Sin embargo, si la aplicación tiene éxito, el volumen de información crece de forma constante:

- más clientes,
- más pedidos,
- más productos,
- más consultas,
- más conexiones simultáneas.

Llega un momento en que los recursos disponibles dejan de ser suficientes.

La solución consiste en **escalar** la infraestructura.

## ¿Qué significa escalar?

Escalar una base de datos consiste en aumentar su capacidad para soportar una mayor carga de trabajo.

Dependiendo del problema, puede ser necesario incrementar:

- la memoria RAM,
- la capacidad de procesamiento,
- el almacenamiento,
- el número de conexiones simultáneas,
- la velocidad de lectura,
- la disponibilidad.

Existen dos estrategias principales:

- Escalabilidad vertical.
- Escalabilidad horizontal.

Ambas persiguen el mismo objetivo, pero lo hacen de formas muy diferentes.

## Escalabilidad vertical

La escalabilidad vertical consiste en **hacer más potente un único servidor**.

Por ejemplo, imaginemos que TechShop utiliza un servidor con:

- 4 núcleos de CPU.
- 16 GB de RAM.
- 500 GB de almacenamiento SSD.

Con el crecimiento de la empresa se decide ampliar sus recursos.

El nuevo servidor dispone de:

- 16 núcleos.
- 64 GB de RAM.
- 2 TB de almacenamiento SSD.

La arquitectura sigue siendo prácticamente la misma, pero el servidor dispone de mayor capacidad.

```text
Antes

Aplicación

      │

Servidor MySQL

4 CPU
16 GB RAM

↓

Después

Aplicación

      │

Servidor MySQL

16 CPU
64 GB RAM
```

No cambia el número de servidores; únicamente aumentan sus recursos.

### Ventajas

- Muy sencilla de implementar.
- Requiere pocos cambios en la aplicación.
- No modifica el modelo de datos.
- Compatible con la mayoría de aplicaciones existentes.

### Inconvenientes

- Existe un límite físico.
- Los servidores muy potentes son costosos.
- Sigue existiendo un único punto de fallo si no se combina con alta disponibilidad.

## Escalabilidad horizontal

La escalabilidad horizontal adopta una estrategia completamente distinta.

En lugar de hacer un servidor más potente, se utilizan **varios servidores trabajando conjuntamente**.

```text
Aplicación

        │

 ┌──────┴──────┐

Servidor A

Servidor B

Servidor C
```

La carga se distribuye entre varias máquinas.

Dependiendo de la arquitectura utilizada, algunos servidores pueden encargarse principalmente de:

- lecturas,
- escrituras,
- réplicas,
- análisis,
- copias de seguridad.

Este modelo es más complejo, pero permite alcanzar capacidades mucho mayores.

## Escalabilidad mediante réplicas de lectura

Una estrategia muy utilizada consiste en mantener un único servidor encargado de las escrituras y varias réplicas destinadas únicamente a consultas.

```text
Escrituras

Aplicación ─────────────► Principal

               │

       Replicación

       ┌───────────────┐

Lecturas         Lecturas

Réplica 1        Réplica 2
```

De esta forma:

- las operaciones `INSERT`, `UPDATE` y `DELETE` llegan al servidor principal,
- mientras que muchas consultas `SELECT` se distribuyen entre las réplicas.

Esto reduce considerablemente la carga sobre el servidor principal.

## Escalabilidad en AWS RDS

Amazon RDS permite ampliar recursos verticalmente modificando el tamaño de la instancia.

También ofrece mecanismos para crear réplicas de lectura que ayudan a distribuir determinadas consultas.

Aunque la configuración concreta depende del servicio contratado, estas funcionalidades simplifican enormemente la ampliación de capacidad.

## Escalabilidad en Google Cloud SQL

Google Cloud SQL proporciona capacidades similares.

Es posible:

- aumentar memoria,
- ampliar almacenamiento,
- utilizar réplicas de lectura,
- adaptar los recursos a las necesidades reales de la aplicación.

La filosofía es muy parecida a la de otros grandes proveedores cloud.

## ¿Cuál es mejor?

No existe una respuesta universal.

### Vertical

Suele ser adecuada cuando:

- la aplicación aún no presenta una carga extremadamente elevada,
- se desea una administración sencilla,
- el crecimiento previsto es moderado.

### Horizontal

Resulta más interesante cuando:

- existen millones de usuarios,
- las consultas aumentan continuamente,
- la disponibilidad es crítica,
- el sistema necesita distribuir la carga entre múltiples servidores.

En muchos proyectos ambas estrategias se utilizan conjuntamente.

## Caso práctico

TechShop comienza con una única instancia MySQL.

Durante los primeros años basta con ampliar la memoria y la CPU.

Posteriormente la empresa abre tiendas en varios países.

El número de consultas aumenta considerablemente.

En ese momento decide incorporar varias réplicas de lectura para repartir parte de la carga.

La evolución se realiza de forma progresiva, sin modificar el modelo relacional diseñado durante el curso.

## Buenas prácticas

- Escalar únicamente cuando exista una necesidad real.
- Supervisar continuamente el consumo de recursos.
- Analizar si el problema se resuelve optimizando consultas antes de ampliar infraestructura.
- Combinar escalabilidad con alta disponibilidad.
- Diseñar pensando en el crecimiento futuro.

## Conclusiones

La escalabilidad permite adaptar una base de datos al crecimiento de una aplicación. La escalabilidad vertical incrementa la capacidad de un único servidor, mientras que la horizontal distribuye la carga entre varios sistemas. Los servicios cloud facilitan ambas estrategias, permitiendo que las aplicaciones evolucionen de forma gradual sin necesidad de rediseñar completamente su arquitectura.

## Ideas clave

- Escalar significa aumentar la capacidad del sistema.
- La escalabilidad vertical mejora un único servidor.
- La escalabilidad horizontal utiliza varios servidores.
- Las réplicas de lectura son una estrategia habitual para distribuir consultas.
- La elección depende del tamaño y las necesidades de cada proyecto.

