# Cálculo de claves

Una vez aprendido el concepto de cierre de atributos, podemos utilizarlo para responder una de las preguntas más importantes del diseño relacional.

> **¿Cómo sabemos si un conjunto de atributos es una clave candidata?**

La respuesta consiste en calcular su cierre.

### Regla general

Un conjunto de atributos será una clave candidata cuando se cumplan dos condiciones.

1. Su cierre contenga todos los atributos de la relación.
2. Sea un conjunto mínimo.

La segunda condición es muy importante.

Si podemos eliminar algún atributo y el cierre sigue siendo completo, entonces no era una clave candidata.

### Ejemplo sencillo

Supongamos una relación con los atributos.

```text
(A, B, C)
```

y las siguientes dependencias.

```text
A → B

B → C
```

Calculemos:

```text
A+
```

Obtenemos.

```text
{A, B, C}
```

Como aparecen todos los atributos de la relación, podemos concluir que:

```text
A
```

es una clave candidata.

### Otro ejemplo

Consideremos ahora:

```text
(A, B, C)
```

con las dependencias:

```text
(A, B) → C
```

Calculemos el cierre de A.

```text
A+
=
{A}
```

No obtenemos todos los atributos.

Probemos con B.

```text
B+
=
{B}
```

Tampoco.

Finalmente calculamos:

```text
(A, B)+
```

Resultado.

```text
{A, B, C}
```

Ahora sí.

La clave candidata será:

```text
(A, B)
```

### Comprobación de minimalidad

Imaginemos ahora:

```text
(A, B, C)
```

Si descubrimos que:

```text
A+
=
{A, B, C}
```

entonces:

```text
(A, B)
```

no puede ser una clave candidata.

Aunque identifique todos los atributos, no es mínima.

B sobra.

### Aplicación en nuestro caso práctico

En la tabla PRODUCTO:

```text
IdProducto

Nombre

Precio

Stock

IdCategoria
```

Sabemos que:

```text
IdProducto+
```

produce todos los atributos.

Por tanto:

```text
IdProducto
```

es la clave candidata elegida como clave primaria.

### Ideas clave

* El cálculo del cierre permite identificar claves candidatas.
* Una clave debe determinar todos los atributos.
* Además debe ser mínima.
* El cierre constituye una herramienta objetiva para verificar diseños.
* Es ampliamente utilizado durante la normalización.

