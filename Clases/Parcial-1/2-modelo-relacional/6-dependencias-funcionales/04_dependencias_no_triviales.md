# Dependencias no triviales

Las dependencias realmente interesantes para el diseño de bases de datos son las ​**dependencias no triviales**​.

Mientras que una dependencia trivial expresa algo evidente, una dependencia no trivial representa una regla real del negocio.

Son precisamente estas dependencias las que utilizaremos para detectar redundancias y aplicar la normalización.

### Definición

Una dependencia funcional es **no trivial** cuando el atributo o conjunto de atributos situado a la derecha **no forma parte** del conjunto situado a la izquierda.

Por ejemplo:

```text
IdCliente → Nombre
```

El atributo **Nombre** no aparece en el lado izquierdo.

Por tanto, se trata de una dependencia no trivial.

### Ejemplos

En nuestro caso de estudio podemos encontrar muchas dependencias de este tipo.

```text
IdProducto → Nombre
```

```text
IdProducto → Precio
```

```text
IdPedido → Fecha
```

```text
IdCategoria → NombreCategoria
```

Todas ellas representan reglas propias del negocio.

### ¿Por qué son importantes?

Supongamos la siguiente tabla.

| IdProducto | Nombre  | Precio |
| ------------ | --------- | -------: |
| 101        | Ratón  |  18.90 |
| 102        | Teclado |  42.50 |

Si observamos que:

```text
IdProducto → Precio
```

podemos afirmar que el precio no debe almacenarse en ninguna otra tabla relacionada con el producto.

Si lo hiciéramos, estaríamos duplicando información.

Las dependencias funcionales nos ayudan precisamente a detectar este tipo de situaciones.

### No dependen de los datos

Imaginemos la siguiente tabla.

| CódigoPostal | Ciudad    |
| --------------- | ----------- |
| 39001         | Santander |
| 39002         | Santander |

Aunque aparezcan varias filas con la misma ciudad, sigue siendo cierto que:

```text
CodigoPostal → Ciudad
```

Cada código postal identifica una ciudad.

Sin embargo, la dependencia inversa no es válida.

```text
Ciudad → CodigoPostal
```

Porque una misma ciudad puede tener muchos códigos postales.

### Resumen visual

| Dependencia          | Tipo       |
| ---------------------- | ------------ |
| A → A               | Trivial    |
| (A, B) → A          | Trivial    |
| A → B               | No trivial |
| IdCliente → Nombre  | No trivial |
| IdProducto → Precio | No trivial |

### Ideas clave

* Las dependencias no triviales representan reglas reales del negocio.
* El lado derecho contiene atributos que no aparecen en el lado izquierdo.
* Constituyen la base del proceso de normalización.
* Permiten detectar redundancias e inconsistencias.
* Son las dependencias que más utilizaremos durante el resto del curso.

