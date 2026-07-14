# Variables locales

## Introducción

Además de los parámetros, los procedimientos pueden utilizar ​**variables locales**​.

Una variable local funciona igual que una variable en cualquier lenguaje de programación.

Sirve para almacenar información temporal mientras el procedimiento se está ejecutando.

Una vez finalizada la ejecución, la variable desaparece.

---

## Declaración

Las variables locales se declaran mediante:

```sql
DECLARE nombre TipoDato;
```

Todas las declaraciones deben situarse al comienzo del bloque `BEGIN...END`, antes de cualquier otra instrucción.

---

## Primer ejemplo

```sql
DELIMITER $$

CREATE PROCEDURE EjemploVariables()

BEGIN

    DECLARE TotalProductos INT;

    SELECT COUNT(*)
    INTO TotalProductos
    FROM Producto;

    SELECT TotalProductos;

END $$

DELIMITER ;
```

En este ejemplo:

* se declara una variable;
* se almacena el número de productos;
* posteriormente se muestra su contenido.

---

## Inicializar una variable

También es posible asignar un valor inicial.

```sql
DECLARE Contador INT DEFAULT 0;
```

O posteriormente mediante:

```sql
SET Contador = 10;
```

---

## Variables y operaciones

Las variables pueden participar en expresiones.

```sql
DECLARE Precio DECIMAL(10,2);

SET Precio = 150;

SET Precio = Precio * 1.21;
```

En este caso se aplica un incremento del 21 %.

---

## Variables y consultas

Es muy frecuente almacenar el resultado de una consulta.

```sql
DECLARE TotalPedidos INT;

SELECT COUNT(*)
INTO TotalPedidos
FROM Pedido;
```

Posteriormente la variable puede utilizarse en cualquier parte del procedimiento.

---

## Diferencia entre parámetros y variables

| Parámetros                                      | Variables locales                  |
| -------------------------------------------------- | ------------------------------------ |
| Se reciben desde el exterior                     | Se crean dentro del procedimiento  |
| Pueden ser`IN`,`OUT`o`INOUT`         | Solo existen durante la ejecución |
| Forman parte de la definición del procedimiento | Son internas al procedimiento      |

En muchos procedimientos se utilizan ambos tipos simultáneamente.

---

## Ejemplo completo

```sql
DELIMITER $$

CREATE PROCEDURE Estadisticas()

BEGIN

    DECLARE TotalClientes INT;
    DECLARE TotalProductos INT;

    SELECT COUNT(*)
    INTO TotalClientes
    FROM Cliente;

    SELECT COUNT(*)
    INTO TotalProductos
    FROM Producto;

    SELECT
        TotalClientes,
        TotalProductos;

END $$

DELIMITER ;
```

Este procedimiento utiliza dos variables para almacenar resultados intermedios antes de devolverlos.

---

## Buenas prácticas

* Declara las variables al principio del procedimiento.
* Utiliza nombres claros y descriptivos.
* Emplea el tipo de dato más adecuado.
* Evita crear variables innecesarias.
* Mantén un ámbito de uso reducido para facilitar la lectura.

---

## Ideas clave

* Las variables locales almacenan información temporal.
* Se declaran mediante `DECLARE`.
* Pueden inicializarse con `DEFAULT` o mediante `SET`.
* Es habitual almacenar en ellas resultados obtenidos con `SELECT ... INTO`.
* Son una herramienta esencial para construir procedimientos más complejos.

