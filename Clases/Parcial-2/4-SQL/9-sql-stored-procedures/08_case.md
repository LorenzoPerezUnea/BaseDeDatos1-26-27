# CASE

## Introducción

Aunque `IF` resulta muy útil, cuando existen muchas alternativas diferentes el código puede volverse difícil de leer.

Observa este ejemplo:

```text
IF ...

ELSEIF ...

ELSEIF ...

ELSEIF ...

ELSEIF ...

ELSE
```

A medida que aumenta el número de condiciones, el procedimiento se vuelve más largo y complicado.

En estos casos es preferible utilizar la estructura ​**CASE**​.

---

## Sintaxis

La forma general es:

```sql
CASE

    WHEN condicion1 THEN

        instrucciones;

    WHEN condicion2 THEN

        instrucciones;

    ELSE

        instrucciones;

END CASE;
```

Cada condición se evalúa en orden hasta encontrar la primera que se cumpla.

---

## Primer ejemplo

Clasificar un pedido según su importe.

```sql
DELIMITER $$

CREATE PROCEDURE ClasificarPedido(

    IN pTotal DECIMAL(10,2)

)

BEGIN

    CASE

        WHEN pTotal >= 1000 THEN

            SELECT 'Pedido muy grande';

        WHEN pTotal >= 500 THEN

            SELECT 'Pedido grande';

        WHEN pTotal >= 100 THEN

            SELECT 'Pedido medio';

        ELSE

            SELECT 'Pedido pequeño';

    END CASE;

END $$

DELIMITER ;
```

Prueba:

```sql
CALL ClasificarPedido(750);
```

Resultado:

```text
Pedido grande
```

---

## CASE con una expresión

También es posible comparar directamente el valor de una variable.

```sql
CASE Estado

    WHEN 'P' THEN
        SELECT 'Pendiente';

    WHEN 'E' THEN
        SELECT 'Enviado';

    WHEN 'C' THEN
        SELECT 'Cancelado';

    ELSE
        SELECT 'Estado desconocido';

END CASE;
```

Esta sintaxis resulta muy cómoda cuando todas las comparaciones se realizan sobre la misma variable.

---

## ¿IF o CASE?

### Utiliza IF cuando:

* existen una o dos condiciones;
* las expresiones son diferentes entre sí;
* la lógica depende de varias variables.

### Utiliza CASE cuando:

* existen muchas alternativas;
* todas comparan el mismo valor;
* quieres mejorar la legibilidad.

En proyectos reales ambas estructuras suelen convivir.

---

## Ejemplo empresarial

Asignar automáticamente un nivel de descuento.

```sql
CASE

    WHEN TotalCompras >= 10000 THEN

        SELECT 'Descuento Platinum';

    WHEN TotalCompras >= 5000 THEN

        SELECT 'Descuento Oro';

    WHEN TotalCompras >= 1000 THEN

        SELECT 'Descuento Plata';

    ELSE

        SELECT 'Sin descuento';

END CASE;
```

Una estructura clara y fácil de mantener.

---

## Buenas prácticas

* Utiliza `CASE` cuando existan muchas alternativas.
* Ordena las condiciones de mayor a menor prioridad.
* Incluye siempre un bloque `ELSE`.
* Evita duplicar condiciones.
* Mantén cada bloque corto y legible.

---

## Ideas clave

* `CASE` es una alternativa más limpia que múltiples `IF`.
* Facilita la lectura cuando existen muchas posibilidades.
* Puede comparar condiciones o directamente el valor de una variable.
* Es muy utilizado para clasificaciones y reglas de negocio.
* Elegir entre `IF` y `CASE` depende de la claridad del código, no del rendimiento.

