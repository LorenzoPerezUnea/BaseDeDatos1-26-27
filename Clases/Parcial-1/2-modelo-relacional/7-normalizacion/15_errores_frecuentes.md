# Errores frecuentes

La normalización es un procedimiento sistemático, pero durante las primeras prácticas es habitual cometer errores de interpretación.

La mayoría de estos errores aparecen porque los estudiantes intentan memorizar las Formas Normales en lugar de comprender el problema que cada una pretende resolver.

A continuación analizaremos los más habituales.

### Error 1. Normalizar sin analizar las dependencias

Uno de los errores más frecuentes consiste en dividir tablas únicamente por intuición.

Por ejemplo, un estudiante puede pensar que una tabla es "demasiado grande" y comenzar a separarla sin ningún criterio.

La normalización no depende del número de columnas.

Depende de las ​**dependencias funcionales**​.

Toda decisión debe estar respaldada por una dependencia funcional claramente identificada.

### Error 2. Crear una tabla para cada atributo

En el extremo opuesto, algunos estudiantes llegan a crear una tabla prácticamente para cada columna.

Por ejemplo:

```text
CLIENTE

IdCliente
Nombre
```

```text
DIRECCION

Direccion
```

Aunque técnicamente sea posible, este diseño no tiene sentido.

Solo deben separarse aquellos atributos que representen entidades independientes o que eliminen dependencias parciales o transitivas.

### Error 3. Pensar que más tablas siempre significa mejor diseño

Una base de datos con cien tablas no es necesariamente mejor que otra con veinte.

El objetivo no consiste en aumentar el número de tablas.

El objetivo consiste en eliminar redundancias innecesarias.

Un modelo excesivamente fragmentado también dificulta el desarrollo y las consultas.

### Error 4. Confundir relaciones con redundancia

No toda repetición implica un mal diseño.

Por ejemplo:

| IdPedido | IdCliente |
| ---------: | ----------: |
|        1 |         5 |
|        2 |         5 |
|        3 |         5 |

El identificador del cliente aparece varias veces.

Sin embargo, esto no constituye una redundancia indebida.

Es una consecuencia natural de la relación entre CLIENTE y PEDIDO.

Lo que no debe repetirse son los datos descriptivos del cliente, como su nombre o dirección.

### Error 5. Intentar alcanzar BCNF desde el principio

Muchos estudiantes descubren la BCNF y quieren aplicarla inmediatamente a cualquier modelo.

No es una buena estrategia.

En la práctica profesional se sigue un proceso progresivo:

1. Primera Forma Normal.
2. Segunda Forma Normal.
3. Tercera Forma Normal.
4. BCNF cuando realmente sea necesaria.

Saltarse etapas suele generar confusión.

### Error 6. Creer que la normalización mejora automáticamente el rendimiento

La normalización mejora el ​**diseño lógico**​, no necesariamente la velocidad de las consultas.

De hecho, una base de datos muy normalizada puede requerir un mayor número de operaciones `JOIN`.

Por ello, en sistemas de gran tamaño puede recurrirse posteriormente a una desnormalización controlada.

### Error 7. Memorizar en lugar de comprender

Este es, probablemente, el error más importante.

Las Formas Normales no deben aprenderse como una lista de reglas.

Cada una responde a una pregunta concreta.

| Forma Normal | Problema que resuelve                      |
| -------------- | -------------------------------------------- |
| 1FN          | Valores no atómicos y grupos repetitivos  |
| 2FN          | Dependencias parciales                     |
| 3FN          | Dependencias transitivas                   |
| BCNF         | Determinantes que no son claves candidatas |

Si comprendemos el problema, la regla resulta casi evidente.

### Recomendaciones

Cuando analices cualquier tabla, sigue siempre este orden.

1. Comprueba que todos los atributos sean atómicos.
2. Identifica la clave primaria.
3. Escribe las dependencias funcionales.
4. Busca dependencias parciales.
5. Busca dependencias transitivas.
6. Verifica si todos los determinantes son claves candidatas.

Este procedimiento evita la mayoría de los errores.

### Ideas clave

* La normalización debe basarse en dependencias funcionales.
* Más tablas no implica necesariamente un mejor diseño.
* No toda repetición constituye redundancia.
* La comprensión es mucho más importante que la memorización.
* Un proceso ordenado facilita enormemente el análisis.

