# Renombramiento (ρ)

## Introducción

Hasta este momento todos los operadores estudiados trabajan directamente con el contenido de las relaciones.

Filtran tuplas.

Seleccionan atributos.

Combinan relaciones.

Sin embargo, existe un operador cuyo propósito es completamente distinto.

El **renombramiento** no modifica los datos.

No elimina información.

No crea nuevas combinaciones.

Su función consiste simplemente en **asignar un nuevo nombre** a una relación o a algunos de sus atributos durante una consulta.

Aunque pueda parecer un operador menor, resulta imprescindible para construir expresiones complejas y, especialmente, para trabajar con varias copias de una misma relación.

---

### La intuición

Imaginemos una empresa en la que queremos comparar dos empleados.

Ambos pertenecen a la relación ​**Empleado**​.

Si escribimos una expresión que utilice dos veces la misma relación, ¿cómo distinguimos una copia de la otra?

Necesitamos asignar nombres temporales.

Por ejemplo:

* Empleado A
* Empleado B

Eso es precisamente lo que permite el operador de renombramiento.

---

### Definición formal

El renombramiento se representa mediante la letra griega ​**rho (ρ)**​.

Su forma general puede expresarse así:

```text
ρ NuevoNombre (Relación)
```

o, cuando también cambian los atributos:

```text
ρ NuevoNombre(A1, A2, A3...) (Relación)
```

El resultado sigue siendo exactamente la misma relación.

Lo único que cambia es el nombre utilizado dentro de la expresión algebraica.

---

### ¿Por qué es necesario?

Consideremos una situación muy sencilla.

La empresa desea obtener una lista formada por:

* empleado;
* supervisor.

Ambos pertenecen a la misma relación ​**Empleado**​.

Sin renombramiento la consulta resultaría ambigua.

¿A qué empleado hace referencia cada atributo?

Mediante el operador ρ podemos crear dos copias conceptuales:

* EmpleadoActual
* Supervisor

A partir de ese momento la consulta puede distinguir perfectamente ambas relaciones.

---

### Renombramiento de atributos

El operador también permite cambiar temporalmente el nombre de determinados atributos.

Por ejemplo, una relación puede contener:

| IdCliente | Nombre | Telefono |

Y otra:

| IdProveedor | Nombre | Telefono |

Si posteriormente deseamos combinar ambas relaciones, puede resultar conveniente renombrar algunos atributos para hacer más clara la consulta.

Es importante recordar que estos cambios son únicamente temporales.

La base de datos original no se modifica.

---

### Aplicación al caso de estudio

Supongamos que más adelante incorporamos una relación **Empleado** con el siguiente atributo:

**IdSupervisor**

Este atributo apunta a otro empleado de la misma tabla.

Para obtener simultáneamente el nombre del empleado y el nombre de su supervisor necesitaremos trabajar con dos copias conceptuales de la misma relación.

El renombramiento hará posible esa operación.

Posteriormente veremos que SQL resuelve exactamente este problema mediante los conocidos ​**alias**​.

---

### Interpretación gráfica

```mermaid
flowchart LR

A[Relación Cliente]

A --> B[ρ ClientesActivos]

B --> C[Nuevo nombre temporal]
```

Obsérvese que la información permanece idéntica.

Solo cambia la forma de referirse a la relación dentro de la expresión.

---

### Relación con SQL

Cuando estudiemos SQL veremos expresiones como:

```sql
FROM Cliente AS C
```

o simplemente:

```sql
FROM Cliente C
```

Ese alias cumple exactamente la misma función que el operador de renombramiento del Álgebra Relacional.

No crea una nueva tabla.

No duplica los datos.

Únicamente asigna un nombre temporal durante la ejecución de la consulta.

---

### Errores frecuentes

Muchos estudiantes creen que el renombramiento modifica la estructura de la base de datos.

No es así.

Su efecto existe únicamente durante la evaluación de la expresión algebraica.

También es frecuente pensar que solo sirve para abreviar nombres.

En realidad, su principal utilidad consiste en eliminar ambigüedades cuando una consulta utiliza varias relaciones con atributos de nombres similares o varias copias de una misma relación.

---

### Ideas clave

* El renombramiento se representa mediante la letra griega ρ.
* Permite asignar nombres temporales a relaciones o atributos.
* No modifica los datos almacenados.
* Resulta esencial para construir consultas complejas y autorrelaciones.
* Constituye la base conceptual de los alias utilizados posteriormente en SQL.

