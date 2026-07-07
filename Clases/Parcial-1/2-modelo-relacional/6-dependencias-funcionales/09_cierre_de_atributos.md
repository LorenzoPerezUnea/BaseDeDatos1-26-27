# Cierre de atributos

Hasta este momento hemos aprendido qué son las dependencias funcionales y cómo identificar claves candidatas de forma intuitiva.

Sin embargo, cuando una tabla contiene muchos atributos y numerosas dependencias, el razonamiento intuitivo deja de ser suficiente.

Necesitamos un procedimiento sistemático.

Ese procedimiento recibe el nombre de ​**cierre de atributos**​.

Es una de las herramientas matemáticas más importantes del diseño relacional.

### ¿Qué es el cierre de atributos?

El **cierre** de un conjunto de atributos es el conjunto de todos los atributos que pueden determinarse utilizando las dependencias funcionales conocidas.

Se representa mediante un superíndice con un signo más.

```text
A+
```

Se lee:

> El cierre de A.

Si el conjunto inicial está formado por varios atributos:

```text
(A, B)+
```

### ¿Para qué sirve?

El cierre de atributos tiene numerosas aplicaciones.

Permite:

* comprobar si un conjunto de atributos es una clave;
* encontrar claves candidatas;
* verificar dependencias funcionales;
* analizar procesos de normalización.

Durante el resto del curso utilizaremos esta técnica constantemente.

### Un ejemplo sencillo

Supongamos las siguientes dependencias.

```text
A → B

B → C

C → D
```

Queremos calcular:

```text
A+
```

Comenzamos con el propio atributo.

```text
A+
=
{A}
```

Como sabemos que:

```text
A → B
```

añadimos B.

```text
{A, B}
```

Después:

```text
B → C
```

obtenemos C.

```text
{A, B, C}
```

Finalmente:

```text
C → D
```

El resultado es:

```text
A+
=
{A, B, C, D}
```

### Interpretación

Esto significa que conocer A es suficiente para conocer todos los demás atributos.

En consecuencia, A podría ser una clave candidata si estos fueran todos los atributos de la relación.

### Un ejemplo del caso práctico

Consideremos la tabla PRODUCTO.

```text
IdProducto → Nombre

IdProducto → Precio

IdProducto → Stock

IdProducto → IdCategoria
```

Calculemos:

```text
IdProducto+
```

El resultado será:

```text
{
IdProducto,
Nombre,
Precio,
Stock,
IdCategoria
}
```

Observamos que el identificador determina todos los atributos de la tabla.

### Ideas clave

* El cierre indica todos los atributos que pueden deducirse a partir de un conjunto inicial.
* Se representa mediante el símbolo ​**+**​.
* Es la principal herramienta para calcular claves candidatas.
* Permite verificar dependencias funcionales.
* Resulta esencial para comprender la normalización.

