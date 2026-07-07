# Claves candidatas

Hasta ahora hemos hablado de claves primarias como si cada tabla tuviera una única posibilidad para identificar sus registros.

Sin embargo, en muchos casos existen **varios conjuntos de atributos** capaces de hacerlo.

Cada uno de ellos recibe el nombre de ​**clave candidata**​.

### ¿Qué es una clave candidata?

Una clave candidata es un conjunto mínimo de atributos que identifica de forma única cada fila de una tabla.

La palabra **mínimo** es muy importante.

Significa que ninguno de sus atributos puede eliminarse sin perder la capacidad de identificación.

### Un ejemplo

Supongamos la siguiente tabla.

| IdEmpleado | DNI | CorreoCorporativo | Nombre |
| ------------ | ----- | ------------------- | -------- |

Si el negocio garantiza que los tres primeros atributos son únicos, entonces existen tres claves candidatas.

```text
IdEmpleado
```

```text
DNI
```

```text
CorreoCorporativo
```

Las tres identifican unívocamente a cada empleado.

### ¿Cuál será la clave primaria?

De entre todas las claves candidatas elegiremos una para convertirla en la ​**clave primaria**​.

Las restantes seguirán siendo candidatas, aunque normalmente se implementarán mediante restricciones `UNIQUE`.

### Ejemplo con clave compuesta

No todas las claves candidatas están formadas por un único atributo.

Por ejemplo:

```text
(Alumno, Asignatura)
```

puede constituir una clave candidata si ningún alumno puede matricularse dos veces en la misma asignatura.

### Clave candidata y clave primaria

Es habitual confundir ambos conceptos.

| Concepto        | Significado                                                 |
| ----------------- | ------------------------------------------------------------- |
| Clave candidata | Puede identificar de forma única una fila.                 |
| Clave primaria  | Es la clave candidata elegida como identificador principal. |

Toda clave primaria fue previamente una clave candidata.

Pero no todas las claves candidatas terminan convirtiéndose en clave primaria.

### Nuestro caso práctico

En nuestra empresa comercial utilizaremos identificadores artificiales como claves primarias.

No obstante, atributos como el DNI de un empleado o el correo corporativo podrían seguir siendo claves candidatas y protegerse mediante restricciones de unicidad.

### Ideas clave

* Una tabla puede tener varias claves candidatas.
* Todas identifican unívocamente los registros.
* Deben ser mínimas.
* Una de ellas se selecciona como clave primaria.
* Las restantes suelen implementarse mediante restricciones `UNIQUE`.

