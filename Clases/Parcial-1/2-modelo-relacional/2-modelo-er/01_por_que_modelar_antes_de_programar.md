# ¿Por qué modelar antes de programar?

Uno de los errores más habituales entre los programadores principiantes consiste en abrir el gestor de bases de datos y comenzar a crear tablas inmediatamente.

Aunque esta estrategia puede funcionar en proyectos muy pequeños, rápidamente aparecen problemas cuando el sistema crece.

Las tablas empiezan a duplicar información, aparecen relaciones inconsistentes y cada modificación obliga a cambiar gran parte del sistema.

Por este motivo, en el desarrollo profesional siempre se dedica una fase previa al ​**modelado**​.

### Construir sin planos

Imaginemos que una empresa decide construir un edificio de oficinas.

¿Comenzarían los albañiles colocando ladrillos desde el primer día?

Evidentemente no.

Antes intervienen arquitectos e ingenieros que elaboran planos detallados.

En esos planos aparecen:

* Las dimensiones del edificio.
* La distribución de las plantas.
* Las instalaciones eléctricas.
* La red de agua.
* Las salidas de emergencia.

Una vez aprobado el diseño comienza la construcción.

Con las bases de datos ocurre exactamente lo mismo.

### Programar demasiado pronto

Cuando empezamos a crear tablas sin haber analizado el problema solemos cometer errores como:

* Crear información duplicada.
* Elegir nombres poco claros.
* Diseñar relaciones incorrectas.
* Omitir datos importantes.
* Almacenar información innecesaria.

Corregir estos errores una vez que la aplicación está en funcionamiento puede resultar muy costoso.

### El proceso profesional

En la mayoría de proyectos el trabajo sigue un orden parecido al siguiente.

```mermaid
flowchart LR

A[Análisis del problema]
-->B[Modelo Conceptual]

B
-->C[Modelo Relacional]

C
-->D[Implementación SQL]

D
-->E[Aplicación]
```

Cada etapa depende de la anterior.

Si el análisis es incorrecto, todos los pasos posteriores heredarán esos errores.

### El modelado reduce costes

Diversos estudios en Ingeniería del Software muestran que corregir un error durante la fase de análisis resulta mucho más barato que hacerlo cuando el sistema ya está en producción.

Por ello, invertir tiempo en diseñar correctamente una base de datos no supone un retraso, sino un ahorro.

### Nuestro caso práctico

Durante este curso seguiremos exactamente esta metodología.

No comenzaremos escribiendo SQL.

Primero analizaremos la empresa comercial.

Después construiremos un modelo conceptual.

Más adelante lo transformaremos en un modelo relacional y, únicamente cuando el diseño sea correcto, comenzaremos a implementar las tablas en MySQL.

Este procedimiento es el mismo que siguen la mayoría de equipos profesionales.

### Ideas clave

* Una base de datos debe diseñarse antes de implementarse.
* El modelado permite detectar errores cuando aún son fáciles de corregir.
* El diseño conceptual actúa como el plano de un edificio.
* Programar demasiado pronto suele producir bases de datos difíciles de mantener.
* Un buen diseño reduce costes y facilita la evolución futura del sistema.

