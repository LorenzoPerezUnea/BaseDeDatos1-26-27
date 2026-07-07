# Dependencias completas

No todas las dependencias funcionales que involucran varios atributos son iguales.

En algunos casos, **todos** los atributos del lado izquierdo son necesarios para determinar el lado derecho.

Cuando esto ocurre hablamos de una ​**dependencia funcional completa**​.

Comprender este concepto será esencial para estudiar la Segunda Forma Normal.

### Un ejemplo

Consideremos la tabla LINEAPEDIDO.

| IdPedido | IdProducto | Cantidad |
| ---------: | -----------: | ---------: |
|       15 |        101 |        2 |
|       15 |        104 |        1 |
|       16 |        101 |        5 |

Sabemos que la clave primaria está formada por dos atributos.

```text
(IdPedido, IdProducto)
```

Ahora observemos la dependencia.

```text
(IdPedido, IdProducto) → Cantidad
```

### ¿Por qué es completa?

Porque ninguno de los dos atributos es suficiente por separado.

Conocer únicamente el pedido no permite saber la cantidad.

Conocer únicamente el producto tampoco.

Solo la combinación de ambos identifica una línea concreta.

Por ello decimos que la dependencia es ​**completa**​.

### Otro ejemplo

Supongamos la tabla MATRÍCULA.

| Alumno | Asignatura     | Nota |
| -------- | ---------------- | -----: |
| Ana    | Bases de Datos |    8 |
| Ana    | Programación  |    9 |
| Luis   | Bases de Datos |    7 |

La dependencia sería:

```text
(Alumno, Asignatura) → Nota
```

Ni el alumno ni la asignatura determinan por sí solos la nota.

Es necesario conocer ambos.

### ¿Por qué son importantes?

Las dependencias completas indican que todos los atributos de una clave compuesta participan realmente en la identificación de cierta información.

Cuando esto no ocurre aparecen las llamadas ​**dependencias parciales**​, que estudiaremos a continuación y que suelen ser una señal de un diseño mejorable.

### Ideas clave

* Una dependencia completa necesita todos los atributos del lado izquierdo.
* Ningún subconjunto determina el atributo dependiente.
* Son habituales cuando existen claves primarias compuestas.
* Constituyen un requisito para alcanzar la Segunda Forma Normal.
* Ayudan a detectar problemas de diseño antes de implementar la base de datos.

