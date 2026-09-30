# Ejercicio 4. Normalización de un sistema de pedidos y distribución

## Enunciado

Una empresa distribuye productos a sus clientes.

Cada cliente puede realizar varios pedidos. Cada pedido contiene varios productos y un producto puede aparecer en muchos pedidos. Los productos pertenecen a categorías. Cada pedido puede generar varios envíos. Un cliente puede tener varios teléfonos.

### Modelo Chen

```mermaid
flowchart LR

    CLI["CLIENTE"]
    PED["PEDIDO"]
    PRO["PRODUCTO"]
    CAT["CATEGORIA"]
    ENV["ENVIO"]

    REAL{"REALIZA"}
    CONT{"CONTIENE"}
    PERT{"PERTENECE"}
    GENERA{"GENERA"}

    ID_C(("id_cliente"))
    NOM_C(("nombre"))
    EMAIL(("email"))
    TEL(("telefono"))

    ID_P(("id_pedido"))
    FECHA(("fecha"))
    ESTADO(("estado"))

    ID_PRO(("id_producto"))
    NOM_PRO(("nombre"))
    PRECIO(("precio_actual"))

    ID_CAT(("id_categoria"))
    NOM_CAT(("nombre_categoria"))

    ID_E(("id_envio"))
    FECHA_E(("fecha_envio"))
    TRANSP(("transportista"))

    CANT(("cantidad"))
    PRECIO_V(("precio_venta"))

    CLI --- ID_C
    CLI --- NOM_C
    CLI --- EMAIL
    CLI --- TEL

    PED --- ID_P
    PED --- FECHA
    PED --- ESTADO

    PRO --- ID_PRO
    PRO --- NOM_PRO
    PRO --- PRECIO

    CAT --- ID_CAT
    CAT --- NOM_CAT

    ENV --- ID_E
    ENV --- FECHA_E
    ENV --- TRANSP

    CLI --- REAL
    REAL --- PED

    PED --- CONT
    CONT --- PRO
    CONT --- CANT
    CONT --- PRECIO_V

    PRO --- PERT
    PERT --- CAT

    PED --- GENERA
    GENERA --- ENV
```

Relación inicial:

```text
PEDIDO_DISTRIBUCION(
    id_pedido,
    fecha,
    estado,
    id_cliente,
    nombre_cliente,
    email_cliente,
    telefono_cliente,
    id_producto,
    nombre_producto,
    precio_actual,
    id_categoria,
    nombre_categoria,
    cantidad,
    precio_venta,
    id_envio,
    fecha_envio,
    transportista
)
```

Dependencias:

```text
id_pedido → fecha, estado, id_cliente

id_cliente → nombre_cliente, email_cliente

id_producto → nombre_producto, precio_actual, id_categoria

id_categoria → nombre_categoria

id_pedido, id_producto → cantidad, precio_venta

id_envio → fecha_envio, transportista
```

Se pide:

1. Identificar el atributo multivaluado.
2. Determinar la clave.
3. Identificar las dependencias parciales.
4. Identificar las dependencias transitivas.
5. Normalizar hasta 3FN.
6. Obtener las relaciones finales.
7. Crear el diagrama relacional con PK, FK, `NULL/NOT NULL` y restricciones.

## Resolución

### 1. Atributo multivaluado

```text
telefono_cliente
```

Se separa:

```text
TELEFONO_CLIENTE(
    id_cliente PK FK,
    telefono PK
)
```

### 2. Clave inicial

Un pedido puede contener varios productos:

```text
PK = (id_pedido, id_producto)
```

### 3. Dependencias parciales

```text
id_pedido → fecha, estado, id_cliente

id_producto → nombre_producto, precio_actual, id_categoria

id_envio → fecha_envio, transportista
```

Los atributos de `id_pedido`, `id_producto` e `id_envio` no dependen de toda la clave.

### 4. Dependencias transitivas

```text
id_cliente → nombre_cliente, email_cliente

id_categoria → nombre_categoria
```

Además:

```text
id_producto → id_categoria
id_categoria → nombre_categoria
```

Por tanto:

```text
id_producto → nombre_categoria
```

es una dependencia transitiva.

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

CATEGORIA(
    id_categoria PK,
    nombre_categoria
)

PRODUCTO(
    id_producto PK,
    nombre_producto,
    precio_actual,
    id_categoria FK
)

PEDIDO(
    id_pedido PK,
    fecha,
    estado,
    id_cliente FK
)

CONTENIDO_PEDIDO(
    id_pedido PK FK,
    id_producto PK FK,
    cantidad,
    precio_venta
)

ENVIO(
    id_envio PK,
    id_pedido FK,
    fecha_envio,
    transportista
)
```

### 6. Diagrama relacional

```mermaid
erDiagram

    CLIENTE ||--o{ TELEFONO_CLIENTE : "tiene"
    CLIENTE ||--o{ PEDIDO : "realiza"
    PEDIDO ||--o{ CONTENIDO_PEDIDO : "contiene"
    PRODUCTO ||--o{ CONTENIDO_PEDIDO : "aparece"
    CATEGORIA ||--o{ PRODUCTO : "clasifica"
    PEDIDO ||--o{ ENVIO : "genera"

    CLIENTE {
        INT id_cliente PK "NOT NULL"
        VARCHAR nombre_cliente "NOT NULL"
        VARCHAR email "NOT NULL, UNIQUE"
    }

    TELEFONO_CLIENTE {
        INT id_cliente PK, FK "NOT NULL"
        VARCHAR telefono PK "NOT NULL"
    }

    CATEGORIA {
        INT id_categoria PK "NOT NULL"
        VARCHAR nombre_categoria "NOT NULL, UNIQUE"
    }

    PRODUCTO {
        INT id_producto PK "NOT NULL"
        VARCHAR nombre_producto "NOT NULL"
        DECIMAL precio_actual "NOT NULL, CHECK >= 0"
        INT id_categoria FK "NOT NULL"
    }

    PEDIDO {
        INT id_pedido PK "NOT NULL"
        DATE fecha "NOT NULL"
        VARCHAR estado "NOT NULL"
        INT id_cliente FK "NOT NULL"
    }

    CONTENIDO_PEDIDO {
        INT id_pedido PK, FK "NOT NULL"
        INT id_producto PK, FK "NOT NULL"
        INT cantidad "NOT NULL, CHECK > 0"
        DECIMAL precio_venta "NOT NULL, CHECK >= 0"
    }

    ENVIO {
        INT id_envio PK "NOT NULL"
        INT id_pedido FK "NOT NULL"
        DATE fecha_envio "NULL"
        VARCHAR transportista "NULL"
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

CATEGORIA
PK: id_categoria
UNIQUE: nombre_categoria

PRODUCTO
PK: id_producto
FK: id_categoria → CATEGORIA(id_categoria)
CHECK: precio_actual >= 0

PEDIDO
PK: id_pedido
FK: id_cliente → CLIENTE(id_cliente)
NOT NULL: fecha, estado, id_cliente

CONTENIDO_PEDIDO
PK: (id_pedido, id_producto)
FK: id_pedido → PEDIDO(id_pedido)
FK: id_producto → PRODUCTO(id_producto)
CHECK: cantidad > 0
CHECK: precio_venta >= 0

ENVIO
PK: id_envio
FK: id_pedido → PEDIDO(id_pedido)
fecha_envio: NULL permitido
transportista: NULL permitido
```

En `CONTENIDO_PEDIDO`, `precio_venta` representa el precio utilizado en ese pedido, no el precio actual del producto.

