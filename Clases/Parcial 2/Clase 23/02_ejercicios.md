## **3. Ejercicio 1 — Venta con control de stock**

**Objetivo:** realizar una venta solo si hay stock suficiente.

```sql
DELIMITER $$

CREATE PROCEDURE verificar_stock_y_transaccion()
BEGIN
  DECLARE stock_actual INT;

  START TRANSACTION;

  -- Leemos el stock actual del producto 1
  SELECT stock INTO stock_actual 
  FROM producto 
  WHERE id_producto = 1 
  FOR UPDATE;

  -- Verificamos la condición
  IF stock_actual <= 0 THEN
      -- Si no hay stock, revertimos la transacción
      ROLLBACK;
      SELECT ' Stock insuficiente, transacción revertida' AS resultado;
  ELSE
      -- Si hay stock, actualizamos y confirmamos
      UPDATE producto 
      SET stock = stock - 1 
      WHERE id_producto = 1;

      COMMIT;
      SELECT ' Transacción completada correctamente' AS resultado;
  END IF;
END $$

DELIMITER ;
```

## **4. Ejercicio 2 — Simular pago y entrega**

**Objetivo:** registrar el pago y confirmar entrega en la misma transacción.

```sql
DELIMITER $$

CREATE PROCEDURE procesar_pago_total (
    IN p_id_venta INT,
    IN p_monto_pago DECIMAL(10,2)
)
BEGIN
    DECLARE total_detalle DECIMAL(10,2);
    DECLARE nuevo_total DECIMAL(10,2);

    START TRANSACTION;

    -- Calcular total desde los detalles
    SELECT SUM(subtotal)
    INTO total_detalle
    FROM detalle_venta
    WHERE id_venta = p_id_venta;

    -- Validar pago suficiente antes de registrar
    IF p_monto_pago < total_detalle THEN
        ROLLBACK;
        SELECT 'Pago insuficiente. Transacción cancelada.' AS resultado;
    ELSE
        -- Registrar el pago
        INSERT INTO pago (id_venta, monto, fecha_pago)
        VALUES (p_id_venta, p_monto_pago, NOW());

        -- Actualizar estado de la venta
        UPDATE venta
        SET total = total_detalle, estado = 'Pagado'
        WHERE id_venta = p_id_venta;

        COMMIT;
        SELECT 'Pago recibido y venta confirmada.' AS resultado;
    END IF;

END$$

DELIMITER ;
```

## **5. Ejercicio 3**

trasferencia bancaria

```sql
DELIMITER $$

CREATE PROCEDURE transferencia (
    IN cuenta_a_id INT,
    IN cuenta_b_id INT,
    IN p_monto_pago DECIMAL(10,2)
)
BEGIN
    DECLARE total_antes_a DECIMAL(10,2);
    DECLARE total_antes_b DECIMAL(10,2);
    DECLARE total_antes DECIMAL(10,2);
    DECLARE total_despues_a DECIMAL(10,2);
    DECLARE total_despues_b DECIMAL(10,2);
    DECLARE total_despues DECIMAL(10,2);

    START TRANSACTION;

    SELECT monto
    INTO total_antes_a
    FROM cuenta
    WHERE id_cuenta = cuenta_a_id
    FOR UPDATE;

    SELECT monto
    INTO total_antes_b
    FROM cuenta
    WHERE id_cuenta = cuenta_b_id
    FOR UPDATE;

    SET total_antes = total_antes_a + total_antes_b;

    IF total_antes_a < p_monto_pago THEN
        ROLLBACK;
        SELECT 'Monto insuficiente. Transacción cancelada.' AS resultado;
    ELSE
        
        UPDATE cuenta
        SET monto = monto - p_monto_pago
        WHERE id_cuenta = cuenta_a_id;

        UPDATE cuenta
        SET monto = monto + p_monto_pago
        WHERE id_cuenta = cuenta_b_id;

        SELECT monto
        INTO total_despues_a
        FROM cuenta
        WHERE id_cuenta = cuenta_a_id;

        SELECT monto
        INTO total_despues_b
        FROM cuenta
        WHERE id_cuenta = cuenta_b_id;

        SET total_despues = total_despues_a + total_despues_b;

        IF total_antes <> total_despues THEN
            ROLLBACK;
            SELECT 'Error en transferencia.' AS resultado;
        ELSE
            COMMIT;
            SELECT 'Transferencia exitosa.' AS resultado;
        END IF;

    END IF;
END $$

DELIMITER ;
```

Nota: el error en clase era porque faltaba un END IF y poner SET en la lineas que asigna valor a variables

## **6. Ejercicio 4 — Uso de SAVEPOINT**

**Objetivo:** revertir parcialmente una transacción.

```sql
START TRANSACTION;
UPDATE producto SET stock = stock - 3 WHERE id_producto = 2;
SAVEPOINT paso1;

UPDATE producto SET precio = precio * 1.1 WHERE id_producto = 3;
SAVEPOINT paso2;

ROLLBACK TO paso1;
COMMIT;
```

