# Limitaciones y alucinaciones

Las herramientas de Inteligencia Artificial son extraordinariamente útiles, pero no son infalibles.

Comprender sus limitaciones es tan importante como conocer sus capacidades.

Uno de los errores más comunes consiste en asumir que toda respuesta generada por una IA es necesariamente correcta. Esta suposición puede conducir a conclusiones equivocadas y, en el ámbito profesional, a errores importantes.

### ¿Qué es una alucinación?

En Inteligencia Artificial se denomina **alucinación** a una respuesta que parece convincente, pero que contiene información incorrecta, inventada o no respaldada por los datos disponibles.

La IA no miente de forma consciente.

Simplemente genera la respuesta que considera más probable según el patrón aprendido durante su entrenamiento.

Por ello, una explicación puede estar perfectamente redactada y, aun así, contener errores.

### Ejemplos de alucinaciones

Una IA podría:

* Inventar una función SQL que no existe.
* Atribuir una característica a MySQL que pertenece a otro gestor de bases de datos.
* Citar un libro inexistente.
* Generar código que parece correcto, pero que no se ejecuta.

Estos errores pueden pasar desapercibidos si el usuario acepta la respuesta sin comprobarla.

### ¿Por qué ocurren?

Los modelos de lenguaje no consultan una base de datos de respuestas correctas.

Su funcionamiento consiste en predecir cuál es la siguiente palabra más probable dentro del contexto de la conversación.

Como consecuencia, pueden producir respuestas muy fluidas incluso cuando la información no es completamente correcta.

### Cómo reducir el riesgo

Existen varias estrategias para minimizar las alucinaciones.

* Proporcionar suficiente contexto.
* Formular preguntas precisas.
* Solicitar explicaciones paso a paso.
* Contrastar la respuesta con la documentación oficial.
* Probar el código generado antes de utilizarlo.

Estas prácticas reducen significativamente la probabilidad de aceptar información incorrecta.

### La documentación oficial sigue siendo la referencia

Durante este curso utilizaremos con frecuencia ChatGPT y otras herramientas de IA.

Sin embargo, cuando exista alguna duda técnica, la referencia principal será siempre:

* La documentación oficial.
* El material del curso.
* Las pruebas realizadas por el propio estudiante.

La IA complementa estas fuentes, pero no las sustituye.

### Caso práctico

Supongamos que ChatGPT genera una consulta SQL para crear una tabla.

Antes de incorporarla a nuestro proyecto deberíamos:

1. Leer la consulta.
2. Comprender cada instrucción.
3. Ejecutarla.
4. Comprobar que produce el resultado esperado.

Solo después de este proceso podremos considerarla una solución válida.

### Ideas clave

* Las respuestas de una IA pueden contener errores.
* Una alucinación es una respuesta aparentemente correcta, pero falsa o inexacta.
* Nunca debe copiarse código sin revisarlo.
* La documentación oficial continúa siendo la fuente de referencia.
* La mejor forma de detectar errores es comprender y probar las soluciones obtenidas.

