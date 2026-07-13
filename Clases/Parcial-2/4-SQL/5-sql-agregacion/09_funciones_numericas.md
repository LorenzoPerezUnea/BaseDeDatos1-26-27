# Funciones numéricas

## Introducción

Las bases de datos no solo almacenan texto.

Gran parte de la información empresarial está formada por números:

* precios;
* salarios;
* descuentos;
* existencias;
* porcentajes;
* cantidades vendidas.

SQL incorpora numerosas funciones para trabajar con este tipo de datos.

Estas funciones permiten redondear, calcular valores absolutos o realizar operaciones matemáticas sin necesidad de programar fuera de la base de datos.

---

## ROUND()

Redondea un número decimal.

```sql
SELECT
    ROUND(Precio,2)
FROM Producto;
```

Resultado:

| Precio |
| -------: |
| 199.99 |
|  25.50 |
| 950.00 |

El segundo parámetro indica el número de decimales.

---

## CEIL()

Devuelve el entero inmediatamente superior.

```sql
SELECT
    CEIL(Precio)
FROM Producto;
```

Ejemplos:

| Valor | CEIL |
| ------: | -----: |
|  25.1 |   26 |
|  25.9 |   26 |
|  25.0 |   25 |

Es muy utilizado cuando siempre queremos redondear hacia arriba.

---

## FLOOR()

Realiza la operación contraria.

```sql
SELECT
    FLOOR(Precio)
FROM Producto;
```

Ejemplos:

| Valor | FLOOR |
| ------: | ------: |
|  25.9 |    25 |
|  25.1 |    25 |
|  25.0 |    25 |

---

## ABS()

Obtiene el valor absoluto.

```sql
SELECT
    ABS(-35);
```

Resultado:

| ABS(-35) |
| ---------: |
|       35 |

Es útil para calcular diferencias o eliminar signos negativos.

---

## MOD()

Calcula el resto de una división.

```sql
SELECT
    MOD(17,5);
```

Resultado:

| MOD(17,5) |
| ----------: |
|         2 |

También puede escribirse:

```sql
SELECT
    17 % 5;
```

---

## POW()

Calcula potencias.

```sql
SELECT
    POW(2,8);
```

Resultado:

| POW(2,8) |
| ---------: |
|      256 |

---

## SQRT()

Calcula la raíz cuadrada.

```sql
SELECT
    SQRT(81);
```

Resultado:

| SQRT(81) |
| ---------: |
|        9 |

---

## Combinando funciones

Las funciones pueden combinarse entre sí.

```sql
SELECT
    ROUND(
        AVG(Precio),
        2
    ) AS PrecioMedio
FROM Producto;
```

En este ejemplo:

1. `AVG()` calcula la media.
2. `ROUND()` redondea el resultado a dos decimales.

Esta combinación es muy habitual en informes financieros.

---

## Aplicaciones reales

Las funciones numéricas aparecen en multitud de escenarios:

* cálculo de descuentos;
* redondeo de impuestos;
* estadísticas;
* indicadores financieros;
* análisis de ventas;
* cálculo de beneficios.

En muchos casos permiten evitar cálculos adicionales en la aplicación.

---

## Ideas clave

* Las funciones numéricas procesan valores numéricos individuales.
* `ROUND()` redondea números.
* `CEIL()` y `FLOOR()` controlan el sentido del redondeo.
* `ABS()` devuelve el valor absoluto.
* `MOD()` obtiene el resto de una división.
* `POW()` y `SQRT()` realizan operaciones matemáticas.
* Estas funciones pueden combinarse con funciones de agregación para generar resultados más precisos.

