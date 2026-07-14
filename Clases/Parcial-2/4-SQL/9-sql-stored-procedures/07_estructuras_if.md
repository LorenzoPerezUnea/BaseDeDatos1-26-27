# Estructuras IF

## Introducción

Hasta ahora nuestros procedimientos ejecutaban siempre las mismas instrucciones.

Sin embargo, en un programa real necesitamos tomar decisiones.

Por ejemplo:

* Si hay stock suficiente, realizar la venta.
* Si el cliente no existe, mostrar un mensaje.
* Si el importe supera un determinado valor, aplicar un descuento.
* Si un empleado está inactivo, impedir determinadas operaciones.

Para ello MySQL incorpora la estructura condicional ​**IF**​, muy similar a la que existe en lenguajes como Java, C, Python o JavaScript.

---

## Sintaxis

La forma general es:

```sql
IF condicion THEN

    instrucciones;

END IF;
```

La condición debe devolver un valor verdadero (`TRUE`) o falso (`FALSE`).

---

## Primer ejemplo

Supongamos que queremos comprobar si existen productos registrados.

```sql
DELIMITER $$

CREATE PROCEDURE ComprobarProductos()

BEGIN

    DECLARE Total INT;

    SELECT COUNT(*)
    INTO Total
    FROM Producto;

    IF Total > 0 THEN

        SELECT 'Existen productos registrados';

    END IF;

END $$

DELIMITER ;
```

Al ejecutar:

```sql
CALL ComprobarProductos();
```

Obtendremos el mensaje únicamente si la condición se cumple.

---

## IF...ELSE

Lo más habitual es disponer de dos caminos posibles.

```sql
IF condicion THEN

    instrucciones;

ELSE

    otras_instrucciones;

END IF;
```

Ejemplo:

```sql
DELIMITER $$

CREATE PROCEDURE RevisarStock(

    IN pStock INT

)

BEGIN

    IF pStock > 0 THEN

        SELECT 'Producto disponible';

    ELSE

        SELECT 'Producto agotado';

    END IF;

END $$

DELIMITER ;
```

Pruebas:

```sql
CALL RevisarStock(25);

CALL RevisarStock(0);
```

---

## IF...ELSEIF

Cuando existen varias posibilidades utilizamos `ELSEIF`.

```sql
IF condicion1 THEN

...

ELSEIF condicion2 THEN

...

ELSE

...

END IF;
```

Ejemplo:

```sql
DELIMITER $$

CREATE PROCEDURE ClasificarNota(

    IN pNota DECIMAL(4,2)

)

BEGIN

    IF pNota >= 9 THEN

        SELECT 'Sobresaliente';

    ELSEIF pNota >= 7 THEN

        SELECT 'Notable';

    ELSEIF pNota >= 5 THEN

        SELECT 'Aprobado';

    ELSE

        SELECT 'Suspenso';

    END IF;

END $$

DELIMITER ;
```

---

## Condiciones complejas

Podemos utilizar operadores lógicos.

```sql
IF Stock > 0 AND Activo = TRUE THEN

    ...

END IF;
```

También:

```sql
IF Precio >= 100 OR Oferta = TRUE THEN

    ...

END IF;
```

Las mismas reglas vistas en `WHERE` siguen siendo válidas.

---

## Caso práctico

Validar una venta.

```sql
IF Cantidad <= Stock THEN

    UPDATE Producto
    SET Stock = Stock - Cantidad
    WHERE IdProducto = pIdProducto;

ELSE

    SELECT 'Stock insuficiente';

END IF;
```

Este tipo de comprobaciones aparece constantemente en aplicaciones empresariales.

---

## Buenas prácticas

* Mantén las condiciones sencillas.
* Evita anidar demasiados `IF`.
* Utiliza nombres de variables descriptivos.
* Si existen muchas alternativas, considera utilizar `CASE`.
* Comenta la lógica cuando sea especialmente compleja.

---

## Ideas clave

* `IF` permite tomar decisiones dentro de un procedimiento.
* Puede utilizarse con `ELSE` y `ELSEIF`.
* Las condiciones funcionan igual que en una cláusula `WHERE`.
* Es una de las estructuras más utilizadas en programación procedimental.
* Permite implementar reglas de negocio directamente en MySQL.

