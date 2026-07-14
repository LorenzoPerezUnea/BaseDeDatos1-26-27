# Parámetros de entrada

## Introducción

Nuestro primer procedimiento siempre devolvía el mismo resultado.

Sin embargo, normalmente queremos que un procedimiento pueda trabajar con distintos datos según la situación.

Para conseguirlo utilizamos ​**parámetros**​.

Un parámetro permite enviar información al procedimiento en el momento de ejecutarlo.

Es el equivalente a los parámetros de una función en lenguajes como Java, C# o Python.

---

## Parámetros IN

Los parámetros de entrada se declaran utilizando la palabra clave:

```sql
IN
```

Su sintaxis general es:

```sql
CREATE PROCEDURE NombreProcedimiento(

    IN parametro TipoDato

)
```

El procedimiento podrá utilizar ese valor durante toda su ejecución.

---

## Primer ejemplo

Queremos buscar un cliente indicando su identificador.

```sql
DELIMITER $$

CREATE PROCEDURE BuscarCliente(

    IN pIdCliente INT

)

BEGIN

    SELECT *
    FROM Cliente
    WHERE IdCliente = pIdCliente;

END $$

DELIMITER ;
```

El parámetro recibe el nombre:

```text
pIdCliente
```

Por convención, muchos desarrolladores utilizan el prefijo **p** para indicar que se trata de un parámetro.

---

## Ejecutar el procedimiento

Podemos buscar distintos clientes simplemente cambiando el valor enviado.

```sql
CALL BuscarCliente(1);
```

o bien:

```sql
CALL BuscarCliente(25);
```

o incluso:

```sql
CALL BuscarCliente(100);
```

El procedimiento es siempre el mismo.

Lo único que cambia es el valor recibido.

---

## Varios parámetros

Un procedimiento puede recibir varios parámetros.

Por ejemplo:

```sql
DELIMITER $$

CREATE PROCEDURE BuscarProducto(

    IN pPrecioMin DECIMAL(10,2),
    IN pPrecioMax DECIMAL(10,2)

)

BEGIN

    SELECT *
    FROM Producto
    WHERE Precio
    BETWEEN pPrecioMin AND pPrecioMax;

END $$

DELIMITER ;
```

Llamada:

```sql
CALL BuscarProducto(50,200);
```

---

## Parámetros de distintos tipos

Los parámetros pueden utilizar prácticamente cualquier tipo de dato.

Por ejemplo:

```sql
IN pNombre VARCHAR(100)

IN pFecha DATE

IN pCantidad INT

IN pPrecio DECIMAL(10,2)

IN pActivo BOOLEAN
```

Su tipo debe ser compatible con el uso que tendrá dentro del procedimiento.

---

## Un ejemplo más completo

Buscar pedidos de un cliente a partir de una fecha.

```sql
DELIMITER $$

CREATE PROCEDURE PedidosCliente(

    IN pCliente INT,
    IN pFecha DATE

)

BEGIN

    SELECT *
    FROM Pedido
    WHERE IdCliente = pCliente
      AND Fecha >= pFecha;

END $$

DELIMITER ;
```

Consulta:

```sql
CALL PedidosCliente(3,'2025-01-01');
```

El mismo procedimiento sirve para miles de consultas distintas.

---

## Buenas prácticas

Cuando utilices parámetros:

* emplea nombres descriptivos;
* utiliza tipos de datos adecuados;
* evita abreviaturas poco claras;
* documenta el significado de cada parámetro;
* valida posteriormente los valores recibidos cuando sea necesario.

---

## Ideas clave

* Los parámetros de entrada utilizan la palabra clave `IN`.
* Permiten reutilizar un mismo procedimiento con diferentes valores.
* Pueden declararse uno o varios parámetros.
* Admiten cualquier tipo de dato soportado por MySQL.
* Constituyen el primer paso para construir procedimientos realmente útiles.

