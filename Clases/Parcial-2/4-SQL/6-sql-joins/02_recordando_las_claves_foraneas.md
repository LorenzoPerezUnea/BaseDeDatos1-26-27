# Recordando las claves foráneas

## Introducción

Los `JOIN` no funcionan por "magia".

Cuando SQL combina dos tablas necesita algún criterio para decidir qué filas están relacionadas entre sí.

Ese criterio suele venir dado por una ​**clave foránea (Foreign Key)**​.

Por este motivo, antes de estudiar los distintos tipos de `JOIN`, conviene recordar cómo funcionan las relaciones entre tablas.

---

## Clave primaria y clave foránea

Recordemos dos conceptos fundamentales.

Una **clave primaria (Primary Key)** identifica de forma única cada fila de una tabla.

Por ejemplo:

### Cliente

| IdCliente | Nombre |
| ----------: | -------- |
|         1 | Ana    |
|         2 | Luis   |
|         3 | Marta  |

Aquí `IdCliente` es la clave primaria.

Ningún cliente puede compartir el mismo identificador.

---

La tabla `Pedido` almacena los pedidos realizados.

### Pedido

| IdPedido | IdCliente | Fecha      |
| ---------: | ----------: | ------------ |
|      101 |         1 | 2026-01-10 |
|      102 |         3 | 2026-01-15 |
|      103 |         1 | 2026-02-02 |

La columna `IdCliente` ya no identifica al pedido.

Su función consiste en indicar ​**a qué cliente pertenece cada pedido**​.

Por ello recibe el nombre de ​**clave foránea**​.

---

## Visualizando la relación

Podemos representar la relación mediante un diagrama sencillo.

```text
Cliente

IdCliente (PK)
Nombre

      ▲
      │
      │
Pedido

IdPedido (PK)
IdCliente (FK)
Fecha
```

La flecha indica que la clave foránea apunta hacia la clave primaria.

---

## Integridad referencial

Las claves foráneas permiten mantener la coherencia de la base de datos.

Por ejemplo, si existe el siguiente pedido:

| IdPedido | IdCliente |
| ---------: | ----------: |
|      101 |         8 |

pero no existe ningún cliente con identificador `8`, la base de datos quedaría en un estado inconsistente.

Para evitarlo, MySQL verifica automáticamente la integridad referencial cuando se han definido correctamente las restricciones `FOREIGN KEY`.

---

## Cómo se crea una clave foránea

Recordemos un ejemplo de la clase anterior.

```sql
CREATE TABLE Pedido (
    IdPedido INT AUTO_INCREMENT,
    Fecha DATE NOT NULL,
    IdCliente INT NOT NULL,

    PRIMARY KEY (IdPedido),

    FOREIGN KEY (IdCliente)
        REFERENCES Cliente(IdCliente)
);
```

A partir de ese momento MySQL conoce que ambas tablas están relacionadas.

Sin embargo, es importante comprender que ​**el hecho de definir una clave foránea no implica que SQL una automáticamente las tablas**​.

La relación existe en el modelo de datos, pero debemos utilizar un `JOIN` cuando queramos consultar información conjunta.

---

## La condición del JOIN

La mayoría de los `JOIN` utilizan precisamente la relación entre la clave primaria y la clave foránea.

```sql
SELECT
    Cliente.Nombre,
    Pedido.IdPedido
FROM Cliente
INNER JOIN Pedido
ON Cliente.IdCliente = Pedido.IdCliente;
```

La cláusula `ON` indica la condición que determina cuándo dos filas deben considerarse relacionadas.

En este caso:

```text
Cliente.IdCliente

=

Pedido.IdCliente
```

Cuando ambos valores coinciden, SQL combina las filas.

---

## ¿Siempre se utilizan claves foráneas?

No necesariamente.

Un `JOIN` puede realizarse utilizando cualquier condición lógica.

Por ejemplo:

```sql
ON Producto.Precio > Oferta.PrecioMinimo
```

o incluso:

```sql
ON YEAR(Pedido.Fecha) = Campaña.Anio
```

No obstante, en la inmensa mayoría de aplicaciones empresariales los `JOIN` se realizan entre claves primarias y claves foráneas.

---

## Buenas prácticas

Cuando diseñes una base de datos:

* define siempre las claves primarias;
* crea las claves foráneas correspondientes;
* utiliza nombres coherentes (`IdCliente`, `IdProducto`, etc.);
* evita relaciones implícitas basadas únicamente en nombres o textos.

Un buen diseño simplifica enormemente la escritura de consultas con `JOIN`.

---

## Ideas clave

* La clave primaria identifica de forma única una fila.
* La clave foránea establece una relación entre tablas.
* Los `JOIN` suelen utilizar la relación entre una clave primaria y una clave foránea.
* La cláusula `ON` especifica cómo deben relacionarse ambas tablas.
* Una buena definición de claves facilita la integridad de los datos y la escritura de consultas.

