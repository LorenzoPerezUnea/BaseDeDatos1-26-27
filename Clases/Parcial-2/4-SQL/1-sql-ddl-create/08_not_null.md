# NOT NULL

## Introducción

En el capítulo anterior vimos que la clave primaria nunca puede contener valores nulos.

Sin embargo, muchas otras columnas también deberían ser obligatorias.

Por ejemplo, ¿tendría sentido almacenar un cliente sin nombre?

¿O registrar un producto cuyo precio fuera desconocido?

En la mayoría de las aplicaciones existen datos imprescindibles para el funcionamiento del sistema. Permitir que esos campos permanezcan vacíos reduciría la calidad de la información almacenada y complicaría enormemente el desarrollo de las aplicaciones.

Para evitar esta situación, SQL proporciona la restricción ​**NOT NULL**​.

---

### ¿Qué significa NULL?

Antes de estudiar `NOT NULL` es importante comprender el significado de `NULL`.

Un valor `NULL`​**no representa cero**​, ni una cadena vacía, ni el texto `"NULL"`.

Representa simplemente que ​**el valor es desconocido o no existe**​.

Por ejemplo:

| Valor | Significado                     |
| ------- | --------------------------------- |
| 0     | El valor es cero                |
| ''    | Cadena vacía                   |
| NULL  | Valor desconocido o inexistente |

Esta diferencia será muy importante cuando aprendamos a realizar consultas utilizando `WHERE`.

---

### Definiendo columnas obligatorias

Supongamos que decidimos que todo cliente debe tener obligatoriamente un nombre y un correo electrónico.

Podemos modificar la creación de la tabla de la siguiente forma.

```sql
DROP TABLE IF EXISTS Cliente;

CREATE TABLE Cliente (

    IdCliente INT PRIMARY KEY,

    Nombre VARCHAR(100) NOT NULL,

    CorreoElectronico VARCHAR(150) NOT NULL,

    Ciudad VARCHAR(80),

    FechaRegistro DATE

);
```

Ahora ambas columnas pasan a ser obligatorias.

---

### Comprobando la estructura

Ejecute:

```sql
DESC Cliente;
```

La salida mostrará:

| Field             | Null |
| ------------------- | ------ |
| IdCliente         | NO   |
| Nombre            | NO   |
| CorreoElectronico | NO   |
| Ciudad            | YES  |
| FechaRegistro     | YES  |

Podemos comprobar visualmente qué columnas admiten valores nulos y cuáles no.

---

### Probando la restricción

Intentemos insertar un cliente omitiendo el nombre.

```sql
INSERT INTO Cliente
VALUES
(
    1,
    NULL,
    'ana@empresa.com',
    'Santander',
    '2026-09-15'
);
```

MySQL responderá con un mensaje similar a:

```text
ERROR 1048 (23000):
Column 'Nombre' cannot be null
```

El registro no será almacenado.

En cambio, sí podremos omitir la ciudad.

```sql
INSERT INTO Cliente
VALUES
(
    1,
    'Ana Ruiz',
    'ana@empresa.com',
    NULL,
    '2026-09-15'
);
```

Esta operación se ejecutará correctamente porque la columna `Ciudad` sigue permitiendo valores nulos.

---

### ¿Qué columnas deberían ser obligatorias?

No existe una respuesta universal.

Depende de las reglas de negocio de cada aplicación.

En nuestro caso práctico, normalmente serán obligatorios:

* identificadores;
* nombres principales;
* precios;
* cantidades;
* fechas esenciales.

En cambio, algunos datos como observaciones, comentarios o direcciones secundarias podrán permanecer vacíos.

El objetivo consiste en impedir únicamente aquellos valores cuya ausencia comprometería el funcionamiento del sistema.

---

### Errores frecuentes

Muchos estudiantes utilizan `NOT NULL` en absolutamente todas las columnas.

Otros hacen exactamente lo contrario y permiten valores nulos en campos esenciales.

El equilibrio consiste en analizar cuidadosamente las necesidades reales del negocio antes de decidir qué información debe ser obligatoria.

### Ideas clave

* `NULL` representa la ausencia o el desconocimiento de un valor.
* `NOT NULL` obliga a proporcionar un dato para una columna determinada.
* La clave primaria siempre implica `NOT NULL`.
* No todas las columnas deben ser obligatorias.
* Las restricciones ayudan a mantener la calidad e integridad de la información almacenada.

