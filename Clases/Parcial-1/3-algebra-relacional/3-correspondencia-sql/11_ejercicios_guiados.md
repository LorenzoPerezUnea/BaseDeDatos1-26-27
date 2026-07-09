# Ejercicios guiados

## Introducción

Después de estudiar la correspondencia entre el Álgebra Relacional y SQL es necesario consolidar los conocimientos mediante ejercicios de traducción. El objetivo de esta sesión no es memorizar la sintaxis de SQL, sino comprobar que el estudiante es capaz de reconocer la misma consulta expresada en dos lenguajes diferentes.

En todos los ejercicios se utilizará el caso práctico desarrollado a lo largo del curso. Las relaciones empleadas serán las mismas que han acompañado al estudiante desde el diseño conceptual hasta el Álgebra Relacional:

* Cliente
* Pedido
* LineaPedido
* Producto
* Categoria
* Proveedor

Se recomienda resolver primero cada ejercicio utilizando Álgebra Relacional y, únicamente después, escribir la consulta equivalente en SQL. Este orden obliga a razonar sobre el problema antes de pensar en la sintaxis.

---

### Ejercicio 1. Clientes de una ciudad

Obtenga el nombre y el correo electrónico de todos los clientes cuya ciudad sea ​**Santander**​.

#### Álgebra Relacional

```text
π Nombre, CorreoElectronico
(
    σ Ciudad='Santander'
    (
        Cliente
    )
)
```

#### SQL

```sql
SELECT Nombre,
       CorreoElectronico
FROM Cliente
WHERE Ciudad='Santander';
```

---

### Ejercicio 2. Productos de una categoría

Obtenga el nombre y el precio de todos los productos pertenecientes a la categoría ​**Monitores**​.

#### Álgebra Relacional

```text
π Nombre, Precio
(
    σ Categoria='Monitores'
    (
        Producto
    )
)
```

#### SQL

```sql
SELECT Nombre,
       Precio
FROM Producto
WHERE Categoria='Monitores';
```

---

### Ejercicio 3. Pedidos realizados por cada cliente

Obtenga el nombre del cliente y la fecha de sus pedidos.

#### Álgebra Relacional

```text
π Cliente.Nombre, Pedido.Fecha
(
    Cliente
    ⋈ Cliente.IdCliente = Pedido.IdCliente
    Pedido
)
```

#### SQL

```sql
SELECT c.Nombre,
       p.Fecha
FROM Cliente c
INNER JOIN Pedido p
    ON c.IdCliente = p.IdCliente;
```

---

### Ejercicio 4. Productos comprados por cada cliente

Obtenga el nombre del cliente y el nombre del producto adquirido.

#### Álgebra Relacional

```text
π Cliente.Nombre,
  Producto.Nombre
(
    Cliente
    ⋈ Pedido
    ⋈ LineaPedido
    ⋈ Producto
)
```

#### SQL

```sql
SELECT c.Nombre,
       pr.Nombre
FROM Cliente c
INNER JOIN Pedido p
    ON c.IdCliente = p.IdCliente
INNER JOIN LineaPedido lp
    ON p.IdPedido = lp.IdPedido
INNER JOIN Producto pr
    ON lp.IdProducto = pr.IdProducto;
```

---

### Ejercicio 5. Consulta combinada

Obtenga el nombre de los clientes de Santander que hayan comprado productos de la categoría ​**Monitores**​.

Antes de escribir la consulta SQL, identifique:

* las relaciones implicadas;
* el recorrido entre ellas;
* los filtros;
* los atributos que deben aparecer en el resultado.

Resuelva primero la consulta mediante Álgebra Relacional y después traduzca el resultado a SQL.

---

### Recomendaciones para resolver los ejercicios

Para todos los ejercicios puede utilizarse siempre la misma estrategia:

1. Identificar qué información debe aparecer en el resultado.
2. Localizar la relación donde se encuentra cada dato.
3. Determinar el recorrido mediante JOIN.
4. Aplicar los filtros necesarios.
5. Realizar la proyección final.

Seguir este procedimiento evita muchos de los errores habituales durante las primeras semanas de trabajo con SQL y ayuda a construir consultas de forma ordenada.

### Ideas clave

* Traducir consultas en ambos sentidos mejora la comprensión del Modelo Relacional.
* La sintaxis cambia, pero la lógica permanece constante.
* Resolver primero el problema mediante Álgebra Relacional suele facilitar la construcción de la consulta SQL.
* Identificar el recorrido entre las relaciones es una parte esencial del proceso.
* Una metodología sistemática reduce los errores y facilita el diseño de consultas complejas.

