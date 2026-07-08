# Desnormalización: cuándo conviene

Hasta ahora podría parecer que cuanto más normalizada esté una base de datos, mejor será.

En términos de calidad del diseño, esto suele ser cierto.

Sin embargo, en sistemas reales interviene otro factor muy importante:

> **El rendimiento.**

En determinadas situaciones, una base de datos completamente normalizada puede requerir demasiadas uniones (`JOIN`) para responder a una consulta.

Cuando esto ocurre, algunos sistemas optan por una ​**desnormalización controlada**​.

### ¿Qué es desnormalizar?

Desnormalizar consiste en introducir deliberadamente cierta redundancia para mejorar el rendimiento de determinadas operaciones.

No significa diseñar mal la base de datos.

Significa aceptar una pequeña duplicación de información porque el beneficio obtenido compensa el coste.

### Un ejemplo

Supongamos las tablas:

```text
CLIENTE
```

```text
PEDIDO
```

```text
LINEAPEDIDO
```

```text
PRODUCTO
```

Para obtener un informe completo quizá sea necesario realizar varios `JOIN`.

Si este informe se ejecuta millones de veces al día, el coste puede ser elevado.

Una solución podría consistir en almacenar también el nombre del cliente dentro de una tabla de resumen.

Aunque exista redundancia, las consultas serán mucho más rápidas.

### ¿Cuándo conviene?

La desnormalización suele utilizarse cuando:

* existen consultas muy frecuentes;
* los datos cambian poco;
* el rendimiento es prioritario;
* el coste de mantener información duplicada es aceptable.

### ¿Cuándo no conviene?

No debería utilizarse:

* durante el diseño inicial;
* para evitar aprender normalización;
* como solución a un modelo incorrecto;
* sin medir previamente el rendimiento.

Primero se diseña correctamente.

Solo después, si aparecen problemas de rendimiento demostrables, se estudia una posible desnormalización.

### Relación con el curso

Durante las primeras fases del curso trabajaremos siempre con modelos normalizados.

Más adelante, cuando estudiemos optimización de consultas e índices, volveremos sobre este concepto desde un punto de vista práctico.

### Ideas clave

* La desnormalización introduce redundancia de forma controlada.
* Su objetivo principal es mejorar el rendimiento.
* Nunca debe sustituir un buen diseño lógico.
* Debe basarse en mediciones reales y no en suposiciones.
* Primero se normaliza; después, si es necesario, se desnormaliza.

