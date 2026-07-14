# Caso práctico: Empresa

## Introducción

Para finalizar la parte práctica de esta clase construiremos un procedimiento almacenado inspirado en una situación real de una empresa.

El objetivo será automatizar el registro de un pedido sencillo.

Aunque en aplicaciones profesionales este proceso suele ser más complejo, el ejemplo reúne muchos de los conceptos estudiados hasta ahora:

* parámetros;
* variables;
* estructuras `IF`;
* consultas;
* actualización de datos.

---

## Situación

Disponemos de dos tablas:

```text
Cliente

Producto
```

Queremos crear un procedimiento que:

1. Reciba el identificador del producto.
2. Reciba la cantidad solicitada.
3. Compruebe el stock disponible.
4. Actualice el inventario si existe suficiente cantidad.
5. Informe del resultado.

---

## Paso 1. Crear el procedimiento

```sql
DELIMITER $$

CREATE PROCEDURE RegistrarVenta(

    IN pIdProducto INT,
    IN pCantidad INT

)

BEGIN

    DECLARE vStock INT;

    SELECT Stock
    INTO vStock
    FROM Producto
    WHERE IdProducto = pIdProducto;
```

Hasta este punto únicamente hemos recuperado el stock del producto.

---

## Paso 2. Validar la cantidad

```sql
IF vStock >= pCantidad THEN
```

Si hay suficiente stock podremos continuar.

En caso contrario se mostrará un mensaje informativo.

---

## Paso 3. Actualizar el inventario

```sql
UPDATE Producto

        SET Stock = Stock - pCantidad

        WHERE IdProducto = pIdProducto;
```

Con esta operación descontamos las unidades vendidas.

---

## Paso 4. Informar del resultado

```sql
SELECT 'Venta registrada correctamente';
```

En caso contrario:

```sql
ELSE

        SELECT 'Stock insuficiente';

    END IF;

END $$

DELIMITER ;
```

---

## Ejecutar el procedimiento

Ejemplo:

```sql
CALL RegistrarVenta(10,3);
```

Si el producto dispone de tres unidades o más:

* el stock disminuirá;
* aparecerá un mensaje de confirmación.

Si no existe suficiente inventario:

* no se modificará la tabla;
* se informará del problema.

---

## Posibles mejoras

Este procedimiento podría ampliarse fácilmente para:

* insertar el pedido en la tabla `Pedido`;
* registrar los detalles de la venta;
* actualizar la fecha de última venta;
* generar un movimiento de almacén;
* escribir un registro en una tabla de auditoría;
* ejecutar todo el proceso dentro de una transacción.

Este tipo de evolución es habitual en aplicaciones empresariales.

---

## Conclusión

Con un único procedimiento hemos automatizado una operación que, de otro modo, requeriría varias consultas ejecutadas en el orden correcto.

Este es precisamente el objetivo de los procedimientos almacenados: ​**encapsular procesos completos para reutilizarlos de forma segura y sencilla**​.

---

## Ideas clave

* Los procedimientos permiten automatizar procesos empresariales.
* Es habitual combinar parámetros, variables y estructuras de control.
* La validación previa evita errores y datos inconsistentes.
* Una única llamada mediante `CALL` puede ejecutar numerosas operaciones SQL.
* Los procedimientos son una pieza fundamental en aplicaciones de gestión y sistemas empresariales.

