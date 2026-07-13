# Funciones de fecha

## Introducción

Las fechas constituyen uno de los tipos de datos más utilizados en cualquier sistema de información.

Prácticamente todas las aplicaciones almacenan información temporal:

* fecha de registro de un cliente;
* fecha de creación de un pedido;
* fecha de contratación de un empleado;
* fecha de emisión de una factura;
* fecha de entrega de un envío.

SQL incorpora numerosas funciones para trabajar con fechas y horas sin necesidad de realizar cálculos manuales.

En este apartado estudiaremos las funciones más utilizadas en MySQL.

---

## NOW()

`NOW()` devuelve la fecha y la hora actuales del servidor.

```sql
SELECT
    NOW() AS FechaHoraActual;
```

Resultado (ejemplo):

| FechaHoraActual     |
| --------------------- |
| 2026-07-13 10:35:42 |

Es una de las funciones más utilizadas para registrar cuándo ocurre una operación.

---

## CURDATE() y CURTIME()

Si únicamente necesitamos la fecha o la hora podemos utilizar funciones específicas.

Obtener la fecha actual.

```sql
SELECT
    CURDATE();
```

Resultado:

| CURDATE()  |
| ------------ |
| 2026-07-13 |

Obtener la hora actual.

```sql
SELECT
    CURTIME();
```

Resultado:

| CURTIME() |
| ----------- |
| 10:35:42  |

---

## YEAR(), MONTH() y DAY()

Estas funciones permiten extraer partes concretas de una fecha.

```sql
SELECT
    YEAR(FechaRegistro) AS Anio,
    MONTH(FechaRegistro) AS Mes,
    DAY(FechaRegistro) AS Dia
FROM Cliente;
```

Resultado:

| Año | Mes | Día |
| -----: | ----: | -----: |
| 2025 |  10 |   18 |
| 2026 |   1 |    7 |
| 2026 |   3 |   14 |

Son muy utilizadas para elaborar estadísticas por años, meses o días.

---

## DATEDIFF()

Calcula la diferencia en días entre dos fechas.

```sql
SELECT
    DATEDIFF(
        CURDATE(),
        FechaRegistro
    ) AS DiasDesdeRegistro
FROM Cliente;
```

Resultado:

| DiasDesdeRegistro |
| ------------------: |
|               253 |
|               187 |
|                92 |

Permite calcular fácilmente la antigüedad de clientes, empleados o pedidos.

---

## DATE\_ADD() y DATE\_SUB()

Estas funciones permiten sumar o restar intervalos de tiempo.

Añadir treinta días.

```sql
SELECT
    DATE_ADD(
        CURDATE(),
        INTERVAL 30 DAY
    ) AS FechaVencimiento;
```

Restar un año.

```sql
SELECT
    DATE_SUB(
        CURDATE(),
        INTERVAL 1 YEAR
    ) AS HaceUnAnio;
```

Resultan muy útiles para calcular vencimientos y periodos.

---

## DATE\_FORMAT()

Permite presentar una fecha con un formato personalizado.

```sql
SELECT
    DATE_FORMAT(
        FechaRegistro,
        '%d/%m/%Y'
    ) AS Fecha
FROM Cliente;
```

Resultado:

| Fecha      |
| ------------ |
| 18/10/2025 |
| 07/01/2026 |

Algunos formatos habituales son:

| Formato  | Significado            |
| ---------- | ------------------------ |
| `%d` | Día                   |
| `%m` | Mes                    |
| `%Y` | Año con cuatro cifras |
| `%H` | Hora                   |
| `%i` | Minutos                |
| `%s` | Segundos               |

---

## Aplicaciones reales

Las funciones de fecha aparecen continuamente en sistemas empresariales.

Por ejemplo:

* pedidos realizados este mes;
* clientes registrados este año;
* contratos que vencen en 30 días;
* empleados con más de cinco años de antigüedad;
* facturas emitidas durante un trimestre.

Prácticamente cualquier informe empresarial utiliza alguna función relacionada con fechas.

---

## Buenas prácticas

Siempre que sea posible:

* almacena las fechas utilizando los tipos `DATE`, `TIME` o `DATETIME`;
* evita guardar fechas como texto;
* utiliza funciones de fecha en lugar de manipular cadenas.

De esta forma las consultas serán más rápidas, seguras y fáciles de mantener.

---

## Ideas clave

* `NOW()` devuelve la fecha y hora actuales.
* `CURDATE()` y `CURTIME()` devuelven únicamente la fecha o la hora.
* `YEAR()`, `MONTH()` y `DAY()` extraen componentes de una fecha.
* `DATEDIFF()` calcula diferencias entre fechas.
* `DATE_ADD()` y `DATE_SUB()` permiten sumar o restar intervalos.
* `DATE_FORMAT()` modifica la presentación de una fecha.

