# CREATE VIEW

## Introducción

Ya sabemos qué es una vista y por qué resulta útil.

Ahora aprenderemos a crear nuestra primera vista utilizando la sentencia ​**`CREATE VIEW`**​.

La sintaxis es muy sencilla y recuerda a la creación de una tabla. La diferencia es que, en lugar de definir columnas y tipos de datos, definimos una consulta `SELECT`.

Una vez creada, la vista podrá utilizarse exactamente igual que una tabla en cualquier consulta.

---

## Sintaxis básica

La forma más sencilla de crear una vista es:

```sql
CREATE VIEW nombre_vista AS
SELECT
    columnas
FROM tabla
WHERE condicion;
```

La parte situada después de `AS` puede contener prácticamente cualquier consulta `SELECT` válida.

---

## Primer ejemplo

Supongamos la siguiente tabla:

```text
Cliente
```

Queremos crear una vista que muestre únicamente los clientes activos.

```sql
CREATE VIEW VistaClientesActivos AS
SELECT
    IdCliente,
    Nombre,
    Email
FROM Cliente
WHERE Activo = TRUE;
```

La vista queda almacenada en la base de datos.

A partir de ese momento podemos consultarla igual que una tabla.

---

## Consultar la vista

Una vez creada, basta con ejecutar:

```sql
SELECT *
FROM VistaClientesActivos;
```

El resultado será exactamente el mismo que ejecutar la consulta original.

---

## Otro ejemplo

Crear una vista con los pedidos realizados junto al nombre del cliente.

```sql
CREATE VIEW VistaPedidosClientes AS
SELECT
    p.IdPedido,
    p.Fecha,
    p.Total,
    c.Nombre
FROM Pedido p
INNER JOIN Cliente c
ON p.IdCliente = c.IdCliente;
```

Ahora podemos escribir simplemente:

```sql
SELECT *
FROM VistaPedidosClientes;
```

Toda la lógica del `JOIN` queda oculta dentro de la vista.

---

## Ejecutando el ejemplo en clase

Durante la sesión crearemos la vista directamente sobre nuestra base de datos.

```sql
CREATE VIEW VistaProductos AS
SELECT
    IdProducto,
    Nombre,
    Precio
FROM Producto;
```

Después comprobaremos su funcionamiento:

```sql
SELECT *
FROM VistaProductos;
```

Y veremos que el resultado coincide con consultar directamente la tabla.

---

## ¿Dónde aparece la vista?

Después de crearla podremos verla en:

### MySQL Workbench

Dentro del esquema de la base de datos aparecerá un apartado denominado ​**Views**​.

```
Empresa

├── Tables
├── Views
│     ├── VistaProductos
│     ├── VistaClientesActivos
│     └── VistaPedidosClientes
```

### phpMyAdmin

En el panel lateral también aparecerá junto al resto de objetos de la base de datos, diferenciada mediante el icono correspondiente.

---

## ¿Qué ocurre si la tabla cambia?

La vista sigue utilizando la consulta almacenada.

Si insertamos nuevos registros:

```sql
INSERT INTO Producto
(Nombre, Precio)
VALUES
('Monitor Curvo', 299.90);
```

y ejecutamos:

```sql
SELECT *
FROM VistaProductos;
```

el nuevo producto aparecerá automáticamente.

Esto demuestra que la vista ​**no almacena una copia de los datos**​, sino que consulta las tablas originales cada vez que se utiliza.

---

## Buenas prácticas

Al crear una vista conviene:

* utilizar nombres descriptivos;
* seleccionar únicamente las columnas necesarias;
* evitar incluir `SELECT *`;
* documentar claramente el propósito de la vista.

Esto facilitará su reutilización por otros desarrolladores.

---

## Ideas clave

* Las vistas se crean mediante `CREATE VIEW`.
* La vista almacena una consulta `SELECT`.
* Después puede utilizarse como si fuera una tabla.
* Los datos siempre proceden de las tablas originales.
* Cualquier modificación en las tablas se refleja automáticamente al consultar la vista.

