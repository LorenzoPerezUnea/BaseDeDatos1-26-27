# Ejercicios 1FN

Después de estudiar la Primera Forma Normal es importante aprender a reconocer cuándo una tabla la incumple.

Los siguientes ejercicios están pensados para desarrollar esa habilidad.

### Ejercicio 1

Analiza la siguiente tabla.

| IdCliente | Nombre | Teléfonos           |
| ----------: | -------- | ---------------------- |
|         1 | Ana    | 612345678, 698765432 |
|         2 | Luis   | 611111111            |

**Preguntas**

1. ¿Cumple la Primera Forma Normal?
2. ¿Qué problema presenta?
3. ¿Cómo la transformarías?

### Solución

No cumple la Primera Forma Normal.

La columna **Teléfonos** contiene varios valores.

Una posible solución sería:

```text
CLIENTE

IdCliente
Nombre
```

```text
TELEFONO_CLIENTE

IdTelefono
Numero
IdCliente
```

---

### Ejercicio 2

Observa la siguiente tabla.

| Cliente | Producto1 | Producto2 | Producto3 |
| --------- | ----------- | ----------- | ----------- |

¿Cumple la Primera Forma Normal?

### Solución

No.

Las columnas representan un grupo repetitivo.

La solución consiste en crear una tabla de detalle.

```text
LINEAPEDIDO

IdPedido
IdProducto
Cantidad
```

---

### Ejercicio 3

Analiza la siguiente tabla.

| IdProducto | Nombre  | Precio |
| ------------ | --------- | -------: |
| 101        | Ratón  |  18.90 |
| 102        | Monitor | 189.00 |

¿Cumple la Primera Forma Normal?

### Solución

Sí.

Cada atributo contiene un único valor y no existen listas ni grupos repetitivos.

---

### Ejercicio 4

¿Qué diseño elegirías?

**Opción A**

| Cliente | Correo1 | Correo2 |

**Opción B**

```text
CLIENTE

IdCliente
Nombre
```

```text
CORREO_CLIENTE

IdCorreo
Correo
IdCliente
```

### Solución

La opción B.

Es flexible, escalable y cumple correctamente la Primera Forma Normal.

### Ideas clave

* Identificar listas dentro de una columna suele ser sencillo.
* Los grupos repetitivos también deben eliminarse.
* La solución habitual consiste en crear nuevas tablas.
* La Primera Forma Normal no elimina toda la redundancia.
* La práctica es la mejor forma de aprender a reconocer estos problemas.

