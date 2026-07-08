# Ejercicios 2FN

La Segunda Forma Normal suele resultar más difícil que la Primera, porque ya no basta con observar los datos. Es necesario analizar las **dependencias funcionales** y comprender qué atributos dependen realmente de la clave primaria.

Los siguientes ejercicios están diseñados para desarrollar esa capacidad de análisis.

### Ejercicio 1

Analiza la siguiente tabla.

| IdPedido | IdProducto | NombreProducto | Cantidad |
| ---------: | -----------: | ---------------- | ---------: |
|        1 |        101 | Ratón         |        2 |
|        1 |        102 | Teclado        |        1 |
|        2 |        101 | Ratón         |        4 |

La clave primaria es:

```text
(IdPedido, IdProducto)
```

**Preguntas**

1. ¿Está en Segunda Forma Normal?
2. ¿Qué dependencia parcial existe?
3. ¿Cómo la dividirías?

### Solución

No está en Segunda Forma Normal.

Existe la dependencia:

```text
IdProducto → NombreProducto
```

NombreProducto depende únicamente de una parte de la clave primaria.

La solución sería:

```text
PRODUCTO

IdProducto
NombreProducto
```

```text
LINEAPEDIDO

IdPedido
IdProducto
Cantidad
```

---

### Ejercicio 2

Analiza la siguiente tabla.

| Alumno | Asignatura    | NombreAlumno | Nota |
| -------- | --------------- | -------------- | -----: |
| Ana    | BD            | Ana          |    8 |
| Ana    | Programación | Ana          |    9 |
| Luis   | BD            | Luis         |    7 |

La clave primaria es:

```text
(Alumno, Asignatura)
```

### Solución

Existe la dependencia:

```text
Alumno → NombreAlumno
```

Por tanto, la tabla no cumple la Segunda Forma Normal.

Debe separarse en:

* ALUMNO
* MATRÍCULA

---

### Ejercicio 3

Analiza esta tabla.

| IdProducto | Nombre | Precio |
| ------------ | -------- | -------: |

¿Cumple la Segunda Forma Normal?

### Solución

Sí.

La clave primaria contiene un único atributo.

No pueden existir dependencias parciales.

### Consejos para detectar problemas

Siempre conviene hacerse estas preguntas.

* ¿La clave primaria está formada por varios atributos?
* ¿Existe algún atributo que dependa solo de una parte de esa clave?
* ¿Ese atributo pertenece realmente a otra entidad?

Si la respuesta es afirmativa, probablemente sea necesario aplicar la Segunda Forma Normal.

### Ideas clave

* La Segunda Forma Normal exige analizar dependencias funcionales.
* Las dependencias parciales son el principal problema.
* Las claves simples siempre cumplen automáticamente la 2FN.
* La práctica facilita identificar rápidamente estos casos.
* La solución habitual consiste en separar entidades diferentes.

