## **Modos de aislamiento de transacciones**

El nivel de aislamiento define cuánto puede afectar una transacción a otra concurrente.

| Nivel de aislamiento | Descripción                                   | Riesgos evitados             |
| ---------------------- | ------------------------------------------------ | ------------------------------ |
| READ UNCOMMITTED     | Lee datos no confirmados (sucios).             | Ninguno                      |
| READ COMMITTED       | Solo lee datos confirmados.                    | Dirty reads                  |
| REPEATABLE READ      | Mantiene las filas leídas bloqueadas.         | Dirty + Non-repeatable reads |
| SERIALIZABLE         | Ejecuta las transacciones de forma secuencial. | Todos los riesgos            |

```sql
SET TRANSACTION ISOLATION LEVEL REPEATABLE READ;
START TRANSACTION;
-- operaciones
COMMIT;
```

## **Ejemplo integral de control de transacciones**

```sql
DELIMITER $$

CREATE PROCEDURE prueba_transaccion_stock()
BEGIN
    DECLARE nuevo_stock INT;
    DECLARE id_pedido_generado INT;

    SET autocommit = 0;

    START TRANSACTION;

    -- Restar stock de dos productos quemados
    UPDATE producto SET stock = stock - 1 WHERE id_producto = 1;
    UPDATE producto SET stock = stock - 2 WHERE id_producto = 2;

    -- Revisar el stock menor de los dos productos
    SELECT MIN(stock) INTO nuevo_stock
    FROM producto
    WHERE id_producto IN (1, 2);

    -- Si el stock quedó negativo, revertimos todo
    IF nuevo_stock < 0 THEN
        ROLLBACK;
        SELECT 'ROLLBACK ejecutado: Stock insuficiente.' AS resultado,
               nuevo_stock AS stock_restante;
    ELSE
        -- Creamos el pedido
        INSERT INTO pedido (id_cliente, fecha, total)
        VALUES (1, NOW(), 300.00);

        SET id_pedido_generado = LAST_INSERT_ID();

        -- Insertamos 2 detalles quemados
        INSERT INTO detalle_pedido (id_pedido, id_producto, cantidad, subtotal)
        VALUES
            (id_pedido_generado, 1, 1, 100.00),
            (id_pedido_generado, 2, 2, 200.00);

        COMMIT;

        SELECT 'COMMIT exitoso: Pedido registrado.' AS resultado,
               id_pedido_generado AS pedido,
               nuevo_stock AS stock_restante;
    END IF;

END $$

DELIMITER ;
```

