# Caso práctico de la empresa

## Introducción

Hasta este momento hemos aprendido la sintaxis de las principales instrucciones del Lenguaje de Manipulación de Datos (DML).

Ahora las aplicaremos sobre la base de datos de la empresa tecnológica que llevamos construyendo desde las clases anteriores.

Nuestro objetivo será poblar por primera vez la base de datos con información suficiente para poder realizar consultas reales en las próximas sesiones.

A partir de este momento prácticamente todas las clases utilizarán este mismo conjunto de datos.

---

## Estado inicial

Partimos del siguiente esquema.

```text
Cliente

- IdCliente (PK)
- Nombre
- CorreoElectronico
- Ciudad
- FechaRegistro
- Activo


Categoria

- IdCategoria (PK)
- Nombre
- Descripcion


Producto

- IdProducto (PK)
- Nombre
- Precio
- Stock
- Activo
- IdCategoria (FK)


Empleado

- IdEmpleado (PK)
- Nombre
- Cargo
- FechaContratacion
- Activo
```

Todas las tablas existen, pero todavía están vacías.

---

## Paso 1. Registrar las categorías

Comenzamos por la tabla padre.

```sql
INSERT INTO Categoria
(
    Nombre,
    Descripcion
)
VALUES
(
    'Portátiles',
    'Equipos portátiles'
),
(
    'Monitores',
    'Pantallas'
),
(
    'Periféricos',
    'Accesorios'
),
(
    'Almacenamiento',
    'SSD y HDD'
);
```

Comprobamos el resultado.

```sql
SELECT *
FROM Categoria;
```

---

## Paso 2. Registrar algunos clientes

```sql
INSERT INTO Cliente
(
    Nombre,
    CorreoElectronico,
    Ciudad,
    FechaRegistro,
    Activo
)
VALUES
(
    'Ana Ruiz',
    'ana@empresa.com',
    'Santander',
    CURRENT_DATE,
    TRUE
),
(
    'Luis Gómez',
    'luis@empresa.com',
    'Bilbao',
    CURRENT_DATE,
    TRUE
),
(
    'María López',
    'maria@empresa.com',
    'Oviedo',
    CURRENT_DATE,
    TRUE
);
```

Verificamos.

```sql
SELECT *
FROM Cliente;
```

---

## Paso 3. Registrar empleados

```sql
INSERT INTO Empleado
(
    Nombre,
    Cargo,
    FechaContratacion,
    Activo
)
VALUES
(
    'Carlos Pérez',
    'Vendedor',
    '2024-02-01',
    TRUE
),
(
    'Laura Martín',
    'Administración',
    '2023-09-10',
    TRUE
);
```

---

## Paso 4. Registrar productos

Ahora sí podemos insertar productos, ya que las categorías existen.

```sql
INSERT INTO Producto
(
    Nombre,
    Precio,
    Stock,
    Activo,
    IdCategoria
)
VALUES
(
    'Ultrabook X15',
    1299.95,
    15,
    TRUE,
    1
),
(
    'Monitor 27"',
    289.50,
    40,
    TRUE,
    2
),
(
    'Ratón inalámbrico',
    39.95,
    80,
    TRUE,
    3
),
(
    'SSD NVMe 1TB',
    119.90,
    35,
    TRUE,
    4
);
```

---

## Paso 5. Actualizar información

El proveedor reduce el precio del monitor.

```sql
UPDATE Producto

SET Precio = 259.90

WHERE IdProducto = 2;
```

Comprobamos.

```sql
SELECT *
FROM Producto;
```

---

## Paso 6. Eliminar un registro

Descubrimos que uno de los clientes fue creado por error.

```sql
DELETE FROM Cliente

WHERE IdCliente = 3;
```

Verificamos nuevamente.

```sql
SELECT *
FROM Cliente;
```

---

## Resultado final

Después de todas estas operaciones la base de datos contiene:

* categorías;
* clientes;
* empleados;
* productos.

Ya disponemos de información suficiente para comenzar a realizar consultas SQL reales.

En las próximas clases utilizaremos continuamente este conjunto de datos para practicar `SELECT`, filtros, ordenaciones, funciones de agregación y posteriormente `JOIN`.

---

## Lo aprendido

En este caso práctico hemos utilizado prácticamente todas las instrucciones estudiadas en la clase:

* `INSERT`
* `INSERT` múltiple
* `UPDATE`
* `DELETE`
* `SELECT` (como herramienta de comprobación)

Este flujo de trabajo reproduce bastante fielmente el funcionamiento diario de una aplicación empresarial.

---

## Ideas clave

* Las tablas deben poblarse respetando el orden impuesto por las claves foráneas.
* Después de cada operación DML es recomendable comprobar el resultado.
* La información insertada servirá como base para todas las consultas de las siguientes clases.
* La manipulación de datos constituye la actividad más frecuente en cualquier sistema de información.

