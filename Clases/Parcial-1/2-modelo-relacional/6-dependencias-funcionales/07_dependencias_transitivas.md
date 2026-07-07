# Dependencias transitivas

Después de eliminar las dependencias parciales aún puede quedar otro problema importante.

Se trata de las ​**dependencias transitivas**​.

Son el objetivo principal de la ​**Tercera Forma Normal (3FN)**​.

### La idea intuitiva

Imaginemos tres atributos.

```text
A → B

B → C
```

Aunque no aparezca explícitamente, podemos deducir que:

```text
A → C
```

La dependencia entre A y C se produce ​**a través de B**​.

Por eso recibe el nombre de dependencia transitiva.

### Un ejemplo empresarial

Supongamos la siguiente tabla.

| IdEmpleado | Departamento | TelefonoDepartamento |
| ------------ | -------------- | ---------------------- |
| 1          | Ventas       | 942111111            |
| 2          | Compras      | 942222222            |
| 3          | Ventas       | 942111111            |

Analicemos las dependencias.

```text
IdEmpleado → Departamento
```

Y también:

```text
Departamento → TelefonoDepartamento
```

Por tanto:

```text
IdEmpleado → TelefonoDepartamento
```

Existe una dependencia transitiva.

### ¿Cuál es el problema?

El teléfono del departamento aparece repetido para todos los empleados del mismo departamento.

Si el número cambia habrá que modificar múltiples registros.

Esto genera:

* redundancia;
* riesgo de inconsistencias;
* mayor coste de mantenimiento.

### La solución

Separar la información en dos tablas.

```text
DEPARTAMENTO

------------------------
IdDepartamento
Nombre
Telefono
```

```text
EMPLEADO

------------------------
IdEmpleado
Nombre
IdDepartamento
```

Ahora el teléfono se almacena una única vez.

### Nuestro caso práctico

En la empresa comercial podríamos encontrar una situación similar si almacenáramos la información de la categoría dentro de PRODUCTO.

Por ejemplo:

```text
IdProducto
NombreProducto
IdCategoria
NombreCategoria
```

En realidad:

```text
IdCategoria → NombreCategoria
```

Por tanto, **NombreCategoria** no debería almacenarse en PRODUCTO.

Debe pertenecer a la tabla CATEGORIA.

### Ideas clave

* Una dependencia transitiva aparece cuando un atributo depende de otro atributo no clave.
* Produce redundancias similares a las dependencias parciales.
* Es el principal objetivo de la Tercera Forma Normal.
* La solución consiste en separar la información en nuevas tablas.
* Reducir dependencias transitivas mejora la consistencia de la base de datos.

