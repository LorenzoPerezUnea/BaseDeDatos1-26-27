# Tercera Forma Normal

Después de aplicar la Segunda Forma Normal, todavía puede quedar un último tipo de redundancia.

Esta aparece cuando un atributo no depende directamente de la clave primaria, sino de otro atributo no clave.

Este problema recibe el nombre de **dependencia transitiva** y es precisamente el objetivo de la ​**Tercera Forma Normal (3FN)**​.

### Requisitos

Una relación está en Tercera Forma Normal cuando:

1. Está en Segunda Forma Normal.
2. No existen dependencias transitivas entre atributos no clave.

En otras palabras:

Todos los atributos no clave deben depender **únicamente** de la clave primaria.

### Un ejemplo

Consideremos la siguiente tabla.

| IdProducto | Nombre  | IdCategoria | NombreCategoria |
| ------------ | --------- | ------------- | ----------------- |
| 101        | Ratón  | 1           | Periféricos    |
| 102        | Monitor | 2           | Pantallas       |

Las dependencias funcionales son:

```text
IdProducto → Nombre

IdProducto → IdCategoria

IdCategoria → NombreCategoria
```

La última dependencia indica que **NombreCategoria** no depende realmente del producto.

Depende de la categoría.

### ¿Cuál es el problema?

Si cien productos pertenecen a la categoría "Periféricos", el nombre de la categoría aparecerá repetido cien veces.

Si el nombre cambia habrá que modificar cien registros.

Esto genera redundancia y riesgo de inconsistencias.

### La solución

Separar la categoría en una tabla independiente.

```text
CATEGORIA

IdCategoria
NombreCategoria
```

```text
PRODUCTO

IdProducto
Nombre
IdCategoria
```

Ahora el nombre de la categoría se almacena una sola vez.

### ¿Qué elimina la 3FN?

La Tercera Forma Normal elimina:

* dependencias transitivas;
* redundancia innecesaria;
* anomalías de actualización asociadas a atributos no clave.

### ¿Qué no elimina?

La 3FN no pretende optimizar consultas.

Su objetivo es mejorar el diseño lógico.

Más adelante veremos que, en algunos casos, puede ser conveniente desnormalizar parcialmente una base de datos por motivos de rendimiento.

### Ideas clave

* La Tercera Forma Normal elimina dependencias transitivas.
* Los atributos no clave deben depender únicamente de la clave primaria.
* La solución consiste en separar las entidades relacionadas.
* La redundancia disminuye considerablemente.
* La mayoría de las bases de datos empresariales trabajan, como mínimo, en Tercera Forma Normal.

