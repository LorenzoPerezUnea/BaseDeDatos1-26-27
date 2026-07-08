# Nombres de tablas

Elegir un buen nombre para una tabla puede parecer un detalle menor, pero constituye una decisión importante.

Los nombres acompañarán a la base de datos durante toda su vida útil y aparecerán en miles de consultas SQL, informes, procedimientos almacenados y aplicaciones.

Un nombre claro facilita la comprensión del modelo y reduce la probabilidad de cometer errores.

### ¿Qué debe representar una tabla?

Cada tabla representa una entidad o un concepto claramente identificable dentro del negocio.

Por ello, su nombre debe reflejar exactamente qué información almacena.

Por ejemplo:

```text
CLIENTE
```

representa clientes.

```text
PRODUCTO
```

representa productos.

```text
PEDIDO
```

representa pedidos.

Cuando un desarrollador lea estos nombres, comprenderá inmediatamente el contenido de cada tabla.

### Singular o plural

Existe un debate habitual sobre si las tablas deben escribirse en singular o en plural.

Por ejemplo:

```text
CLIENTE
```

o bien

```text
CLIENTES
```

Ambas opciones son válidas.

Lo importante es mantener la misma convención en toda la base de datos.

En este curso utilizaremos ​**nombres en singular**​, ya que cada fila representa una única instancia de la entidad.

Así, una fila de CLIENTE representa un cliente concreto, una fila de PRODUCTO representa un producto y una fila de PEDIDO representa un pedido.

### Utilizar nombres descriptivos

Los nombres deben ser lo suficientemente descriptivos para evitar dudas.

Es preferible:

```text
LINEA_PEDIDO
```

que:

```text
LINEA
```

El segundo nombre resulta ambiguo.

### Evitar abreviaturas innecesarias

Las abreviaturas pueden ahorrar algunos caracteres, pero suelen dificultar la lectura.

Por ejemplo:

```text
PRD
```

no es tan claro como:

```text
PRODUCTO
```

Actualmente el coste de escribir unos pocos caracteres más es insignificante comparado con el beneficio de tener un código fácil de entender.

### Evitar caracteres especiales

Una buena práctica consiste en utilizar únicamente:

* letras;
* números cuando sean necesarios;
* guion bajo (`_`) si mejora la legibilidad.

No es recomendable utilizar:

* espacios;
* acentos;
* signos de puntuación;
* caracteres especiales.

Por ejemplo:

```text
LINEA_PEDIDO
```

es preferible a:

```text
Línea Pedido
```

### Mantener una convención

Todas las tablas deberían seguir el mismo estilo.

Por ejemplo:

```text
CLIENTE

PRODUCTO

CATEGORIA

PEDIDO

LINEA_PEDIDO

PROVEEDOR
```

Una convención uniforme facilita enormemente la lectura del esquema.

### Ideas clave

* Cada tabla representa una entidad del negocio.
* Los nombres deben ser claros y descriptivos.
* Es importante mantener una única convención.
* Deben evitarse abreviaturas y caracteres especiales.
* La consistencia es más importante que la convención elegida.

