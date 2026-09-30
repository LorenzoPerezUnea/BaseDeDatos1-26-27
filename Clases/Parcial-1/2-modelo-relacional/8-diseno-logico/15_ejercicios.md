# Ejercicio 3. Normalización de un sistema de reservas hoteleras

## Enunciado

Un hotel gestiona clientes, habitaciones y reservas.

Un cliente puede realizar varias reservas y una reserva puede incluir varias habitaciones. Una habitación pertenece a un tipo. Un cliente puede tener varios teléfonos.

### Modelo Chen

```mermaid
flowchart LR

    CLI["CLIENTE"]
    RES["RESERVA"]
    HAB["HABITACION"]
    TIP["TIPO_HABITACION"]

    REAL{"REALIZA"}
    INCLUYE{"INCLUYE"}
    ES{"ES_DE_TIPO"}

    ID_C(("id_cliente"))
    NOM_C(("nombre"))
    EMAIL(("email"))
    TEL(("telefono"))

    ID_R(("id_reserva"))
    FECHA_R(("fecha_reserva"))
    ENTRADA(("fecha_entrada"))
    SALIDA(("fecha_salida"))

    ID_H(("id_habitacion"))
    NUM(("numero"))
    PISO(("piso"))

    ID_T(("id_tipo"))
    DESC(("descripcion"))
    PRECIO(("precio_noche"))

    ADULTOS(("adultos"))
    PRECIO_RES(("precio_aplicado"))

    CLI --- ID_C
    CLI --- NOM_C
    CLI --- EMAIL
    CLI --- TEL

    RES --- ID_R
    RES --- FECHA_R
    RES --- ENTRADA
    RES --- SALIDA

    HAB --- ID_H
    HAB --- NUM
    HAB --- PISO

    TIP --- ID_T
    TIP --- DESC
    TIP --- PRECIO

    CLI --- REAL
    REAL --- RES

    RES --- INCLUYE
    INCLUYE --- HAB
    INCLUYE --- ADULTOS
    INCLUYE --- PRECIO_RES

    HAB --- ES
    ES --- TIP
```

Se dispone de la siguiente relación:

```text
RESERVA_HOTEL(
    id_reserva,
    fecha_reserva,
    fecha_entrada,
    fecha_salida,
    id_cliente,
    nombre_cliente,
    email_cliente,
    telefono_cliente,
    id_habitacion,
    numero_habitacion,
    piso,
    id_tipo,
    descripcion_tipo,
    precio_noche,
    adultos,
    precio_aplicado
)
```

Dependencias:

```text
id_reserva → fecha_reserva, fecha_entrada, fecha_salida, id_cliente

id_cliente → nombre_cliente, email_cliente

id_habitacion → numero_habitacion, piso, id_tipo

id_tipo → descripcion_tipo, precio_noche

id_reserva, id_habitacion → adultos, precio_aplicado
```

Se pide:

1. Identificar el atributo multivaluado.
2. Determinar la clave de la relación inicial.
3. Identificar las dependencias parciales.
4. Identificar las dependencias transitivas.
5. Normalizar hasta 3FN.
6. Indicar las relaciones resultantes.
7. Representar el modelo relacional mediante Mermaid, indicando PK, FK, `NULL/NOT NULL` y restricciones.

## Resolución

### 1. Atributo multivaluado

El teléfono del cliente puede tener varios valores:

```text
telefono_cliente
```

Se crea:

```text
TELEFONO_CLIENTE(
    id_cliente PK FK,
    telefono PK
)
```

### 2. Clave inicial

Una reserva puede incluir varias habitaciones:

```text
PK = (id_reserva, id_habitacion)
```

### 3. Dependencias parciales

```text
id_reserva → fecha_reserva, fecha_entrada, fecha_salida, id_cliente

id_habitacion → numero_habitacion, piso, id_tipo
```

Ambas dependen solamente de una parte de la clave compuesta.

### 4. Dependencias transitivas

```text
id_cliente → nombre_cliente, email_cliente

id_habitacion → id_tipo

id_tipo → descripcion_tipo, precio_noche
```

Por tanto existen dependencias transitivas.

### 5. Relaciones en 3FN

```text
CLIENTE(
    id_cliente PK,
    nombre_cliente,
    email
)

TELEFONO_CLIENTE(
    id_cliente PK FK,
    telefono PK
)

TIPO_HABITACION(
    id_tipo PK,
    descripcion,
    precio_noche
)

HABITACION(
    id_habitacion PK,
    numero,
    piso,
    id_tipo FK
)

RESERVA(
    id_reserva PK,
    fecha_reserva,
    fecha_entrada,
    fecha_salida,
    id_cliente FK
)

INCLUYE(
    id_reserva PK FK,
    id_habitacion PK FK,
    adultos,
    precio_aplicado
)
```

### 6. Diagrama relacional

```mermaid
erDiagram

    CLIENTE ||--o{ TELEFONO_CLIENTE : "tiene"
    CLIENTE ||--o{ RESERVA : "realiza"
    RESERVA ||--o{ INCLUYE : "incluye"
    HABITACION ||--o{ INCLUYE : "aparece"
    TIPO_HABITACION ||--o{ HABITACION : "clasifica"

    CLIENTE {
        INT id_cliente PK "NOT NULL"
        VARCHAR nombre_cliente "NOT NULL"
        VARCHAR email "NOT NULL, UNIQUE"
    }

    TELEFONO_CLIENTE {
        INT id_cliente PK, FK "NOT NULL"
        VARCHAR telefono PK "NOT NULL"
    }

    TIPO_HABITACION {
        INT id_tipo PK "NOT NULL"
        VARCHAR descripcion "NOT NULL, UNIQUE"
        DECIMAL precio_noche "NOT NULL, CHECK > 0"
    }

    HABITACION {
        INT id_habitacion PK "NOT NULL"
        INT numero "NOT NULL, UNIQUE"
        INT piso "NOT NULL"
        INT id_tipo FK "NOT NULL"
    }

    RESERVA {
        INT id_reserva PK "NOT NULL"
        DATE fecha_reserva "NOT NULL"
        DATE fecha_entrada "NOT NULL"
        DATE fecha_salida "NOT NULL, CHECK > entrada"
        INT id_cliente FK "NOT NULL"
    }

    INCLUYE {
        INT id_reserva PK, FK "NOT NULL"
        INT id_habitacion PK, FK "NOT NULL"
        INT adultos "NOT NULL, CHECK > 0"
        DECIMAL precio_aplicado "NOT NULL, CHECK > 0"
    }
```

### Restricciones principales

```text
CLIENTE
PK: id_cliente
UNIQUE: email

TELEFONO_CLIENTE
PK: (id_cliente, telefono)
FK: id_cliente → CLIENTE(id_cliente)

TIPO_HABITACION
PK: id_tipo
UNIQUE: descripcion
CHECK: precio_noche > 0

HABITACION
PK: id_habitacion
FK: id_tipo → TIPO_HABITACION(id_tipo)
UNIQUE: numero

RESERVA
PK: id_reserva
FK: id_cliente → CLIENTE(id_cliente)
CHECK: fecha_salida > fecha_entrada

INCLUYE
PK: (id_reserva, id_habitacion)
FK: id_reserva → RESERVA(id_reserva)
FK: id_habitacion → HABITACION(id_habitacion)
CHECK: adultos > 0
CHECK: precio_aplicado > 0
```

