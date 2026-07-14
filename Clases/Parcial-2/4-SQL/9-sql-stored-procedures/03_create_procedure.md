# CREATE PROCEDURE

## Introducción

Una vez comprendido qué es un procedimiento almacenado y por qué resulta útil, estamos preparados para crear el primero.

En MySQL, los procedimientos se crean mediante la instrucción:

```sql
CREATE PROCEDURE
```

Al igual que una tabla se crea una sola vez y luego puede utilizarse tantas veces como sea necesario, un procedimiento también se almacena dentro de la base de datos para ejecutarlo posteriormente mediante `CALL`.

---

## Sintaxis básica

La forma más sencilla de crear un procedimiento es:

```sql
CREATE PROCEDURE NombreProcedimiento()
BEGIN

    -- Instrucciones SQL

END;
```

Observa dos elementos nuevos:

* `BEGIN`
* `END`

Entre ambas palabras se escriben todas las instrucciones que formarán parte del procedimiento.

---

## El problema del delimitador

Antes de crear procedimientos debemos conocer un detalle muy importante de MySQL.

Normalmente una sentencia SQL termina con:

```sql
;
```

Sin embargo, dentro de un procedimiento también existen instrucciones que terminan con `;`.

Por ejemplo:

```sql
SELECT * FROM Cliente;
SELECT * FROM Producto;
```

Si utilizáramos el delimitador habitual, MySQL pensaría que el procedimiento termina en la primera sentencia.

Para evitarlo cambiamos temporalmente el delimitador.

---

## Utilizando DELIMITER

La forma habitual es:

```sql
DELIMITER $$

CREATE PROCEDURE ListarClientes()
BEGIN

    SELECT *
    FROM Cliente;

END $$

DELIMITER ;
```

Una vez creado el procedimiento restauramos el delimitador original.

Este es un paso obligatorio cuando trabajamos con procedimientos, funciones y triggers en MySQL.

---

## Nuestro primer procedimiento

Vamos a crear un procedimiento muy sencillo.

```sql
DELIMITER $$

CREATE PROCEDURE ListarProductos()
BEGIN

    SELECT *
    FROM Producto;

END $$

DELIMITER ;
```

El procedimiento queda almacenado en la base de datos.

Todavía no se ha ejecutado.

---

## Ejecutar un procedimiento

Para utilizarlo empleamos la instrucción:

```sql
CALL ListarProductos();
```

El resultado será exactamente el mismo que ejecutar:

```sql
SELECT *
FROM Producto;
```

La diferencia es que ahora la consulta está encapsulada dentro del procedimiento.

---

## Un procedimiento con varias instrucciones

Una de las principales ventajas de los procedimientos es que pueden contener varias sentencias.

```sql
DELIMITER $$

CREATE PROCEDURE InformacionEmpresa()
BEGIN

    SELECT COUNT(*) AS TotalClientes
    FROM Cliente;

    SELECT COUNT(*) AS TotalProductos
    FROM Producto;

END $$

DELIMITER ;
```

Al ejecutarlo:

```sql
CALL InformacionEmpresa();
```

MySQL devolverá dos conjuntos de resultados consecutivos.

---

## Mostrar los procedimientos existentes

Podemos consultar los procedimientos almacenados en la base de datos mediante:

```sql
SHOW PROCEDURE STATUS;
```

O limitar la búsqueda a una base de datos concreta:

```sql
SHOW PROCEDURE STATUS
WHERE Db = 'Empresa';
```

En MySQL Workbench y phpMyAdmin también aparecerán dentro del apartado ​**Stored Procedures**​.

---

## Eliminar un procedimiento

Si ya no es necesario:

```sql
DROP PROCEDURE ListarProductos;
```

Después de ejecutarlo, el procedimiento desaparecerá de la base de datos.

---

## Ideas clave

* Los procedimientos se crean mediante `CREATE PROCEDURE`.
* Su contenido se escribe entre `BEGIN` y `END`.
* En MySQL es necesario utilizar `DELIMITER`.
* Se ejecutan mediante `CALL`.
* Pueden contener una o varias instrucciones SQL.

