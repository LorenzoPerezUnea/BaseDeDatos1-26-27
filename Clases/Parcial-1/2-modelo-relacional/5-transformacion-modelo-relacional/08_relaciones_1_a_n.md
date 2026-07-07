# Relaciones 1 a N

La relación **uno a muchos (1:N)** es, con diferencia, la más importante de todo el Modelo Relacional.

La mayoría de las relaciones presentes en una base de datos empresarial pertenecen a esta categoría.

Por este motivo, comprender correctamente su transformación resulta imprescindible.

### Recordando la relación

Supongamos el siguiente modelo conceptual.

```mermaid
erDiagram

CLIENTE ||--o{ PEDIDO : realiza
```

Sabemos que:

* un cliente puede realizar muchos pedidos;
* cada pedido pertenece únicamente a un cliente.

La pregunta ahora es:

> ¿Cómo representamos esta relación mediante tablas?

### La regla fundamental

La respuesta es una de las reglas más importantes del Modelo Relacional.

> **La clave primaria del lado "uno" pasa como clave foránea al lado "muchos".**

En otras palabras:

```text
CLIENTE

IdCliente

↓

PEDIDO

IdCliente
```

El identificador del cliente se copia dentro de la tabla de pedidos.

### Resultado

El modelo relacional quedaría así.

```text
CLIENTE

--------------------------
IdCliente
Nombre
Telefono

PEDIDO

--------------------------
IdPedido
Fecha
Estado
IdCliente
```

Ahora cada pedido sabe exactamente a qué cliente pertenece.

### ¿Por qué se coloca en el lado "muchos"?

Imaginemos la alternativa.

Si almacenáramos todos los pedidos dentro del cliente tendríamos una estructura como esta.

```text
Cliente

Pedido1

Pedido2

Pedido3

Pedido4
```

Este diseño sería imposible de mantener.

No sabemos cuántos pedidos tendrá cada cliente.

Sin embargo, cada pedido sí conoce perfectamente quién es su cliente.

Por eso la clave foránea siempre viaja hacia el lado "muchos".

### Otros ejemplos

La misma regla aparece constantemente.

| Relación                | Clave foránea             |
| -------------------------- | ---------------------------- |
| Categoría → Producto   | IdCategoria en Producto    |
| Departamento → Empleado | IdDepartamento en Empleado |
| Cliente → Pedido        | IdCliente en Pedido        |
| Profesor → Curso        | IdProfesor en Curso        |

Todas siguen exactamente el mismo patrón.

### Caso práctico

Nuestro modelo empezará a transformarse de la siguiente manera.

```text
CLIENTE

IdCliente

...

PEDIDO

IdPedido
Fecha
Estado
IdCliente
```

En la próxima clase implementaremos esta estructura utilizando SQL y claves foráneas reales en MySQL.

### Ideas clave

* La relación 1:N es la más utilizada en bases de datos.
* La clave primaria del lado "uno" pasa al lado "muchos".
* Esa nueva columna recibe el nombre de clave foránea.
* La regla evita redundancias y facilita las consultas.
* Comprender esta transformación es esencial para trabajar con bases de datos relacionales.

