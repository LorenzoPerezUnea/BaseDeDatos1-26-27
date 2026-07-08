# Forma Normal de Boyce-Codd (BCNF)

Después de estudiar la Tercera Forma Normal podría parecer que el proceso de normalización ha terminado. Sin embargo, existen algunos modelos muy particulares que, aun cumpliendo la 3FN, todavía presentan redundancias.

Para resolver estas situaciones aparece la ​**Forma Normal de Boyce-Codd**​, conocida habitualmente como ​**BCNF**​.

Debe su nombre a los investigadores Raymond F. Boyce y Edgar F. Codd.

### ¿Por qué fue necesaria?

La Tercera Forma Normal elimina las dependencias transitivas, pero permite algunas excepciones relacionadas con las claves candidatas.

En la mayoría de las aplicaciones esto no supone ningún problema.

Sin embargo, existen modelos donde esas excepciones siguen produciendo redundancia.

BCNF elimina también esos casos.

### Definición

Una relación está en **Forma Normal de Boyce-Codd** cuando:

> **Todo determinante es una clave candidata.**

La palabra **determinante** hace referencia al conjunto de atributos situado a la izquierda de una dependencia funcional.

Si tenemos:

```text
A → B
```

entonces **A** es el determinante.

BCNF exige que cualquier determinante sea capaz de identificar de forma única una fila.

### Un ejemplo

Supongamos una universidad con la siguiente relación.

| Profesor | Asignatura | Aula |
| ---------- | ------------ | ------ |

Y las dependencias:

```text
Profesor → Aula

(Profesor, Asignatura) → Aula
```

Si un profesor siempre imparte clase en la misma aula, entonces:

```text
Profesor → Aula
```

Pero **Profesor** no identifica completamente un registro, ya que un profesor puede impartir varias asignaturas.

Por tanto, el determinante no es una clave candidata.

La tabla viola BCNF.

### La solución

Separar la información.

```text
PROFESOR

Profesor
Aula
```

```text
DOCENCIA

Profesor
Asignatura
```

Ahora cada dependencia queda correctamente representada.

### ¿Es habitual?

No demasiado.

La inmensa mayoría de los modelos empresariales correctamente diseñados en Tercera Forma Normal también cumplen BCNF.

Sin embargo, conocer esta forma normal ayuda a comprender mejor la teoría del Modelo Relacional.

### Ideas clave

* BCNF es más estricta que la Tercera Forma Normal.
* Todo determinante debe ser una clave candidata.
* Resuelve algunos casos especiales que la 3FN permite.
* En la práctica aparece con poca frecuencia.
* Comprender BCNF proporciona una visión más completa del diseño relacional.

