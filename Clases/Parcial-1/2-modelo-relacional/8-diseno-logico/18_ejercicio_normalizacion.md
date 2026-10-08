# Normalización desde tablas desnormalizadas

## Ejercicio 1. Pedidos de una tienda

### Enunciado

Se dispone de la siguiente tabla desnormalizada:

```
PEDIDOS(
    id_pedido,
    fecha_pedido,
    id_cliente,
    nombre_cliente,
    telefono_cliente,
    productos,
    cantidades,
    precios
)
```

Ejemplo:

```
id_pedido: 1001
fecha_pedido: 2026-10-01
id_cliente: 25
nombre_cliente: Ana García
telefono_cliente: 600111222
productos: P10, P15, P20
cantidades: 2, 1, 4
precios: 15.00, 8.50, 3.20
```

Se sabe que:

```
id_pedido → fecha_pedido, id_cliente
id_cliente → nombre_cliente, telefono_cliente
(id_pedido, id_producto) → cantidad, precio
```

### Se pide

1. Identificar los atributos no atómicos.
2. Transformar la tabla a 1FN.
3. Determinar la clave primaria de la relación en 1FN.
4. Identificar las dependencias parciales.
5. Obtener las relaciones en 2FN.
6. Identificar las dependencias transitivas.
7. Obtener las relaciones finales en 3FN.
8. Indicar PK y FK.

### Resolución

#### 1. 1FN

`<span>productos</span>`, `<span>cantidades</span>` y `<span>precios</span>` contienen varios valores.

Se transforma en:

```
PEDIDO_PRODUCTO(
    id_pedido,
    id_producto,
    fecha_pedido,
    id_cliente,
    nombre_cliente,
    telefono_cliente,
    cantidad,
    precio
)
```

Clave:

```
PK = (id_pedido, id_producto)
```

#### 2. 2FN

Dependencias parciales:

```
id_pedido → fecha_pedido, id_cliente
id_producto → precio
```

Separamos:

```
PEDIDO(
    id_pedido PK,
    fecha_pedido,
    id_cliente,
    nombre_cliente,
    telefono_cliente
)

PRODUCTO(
    id_producto PK,
    precio
)

DETALLE_PEDIDO(
    id_pedido PK FK,
    id_producto PK FK,
    cantidad
)
```

#### 3. 3FN

Existe:

```
id_cliente → nombre_cliente, telefono_cliente
```

Por tanto:

```
PEDIDO(
    id_pedido PK,
    fecha_pedido,
    id_cliente FK
)

CLIENTE(
    id_cliente PK,
    nombre_cliente,
    telefono_cliente
)

PRODUCTO(
    id_producto PK,
    precio
)

DETALLE_PEDIDO(
    id_pedido PK FK,
    id_producto PK FK,
    cantidad
)
```

Resultado: todas las relaciones están en 3FN.

## Ejercicio 2. Gestión de cursos

### Enunciado

Se dispone de:

```
MATRICULAS(
    id_alumno,
    nombre_alumno,
    email,
    asignaturas,
    profesores,
    aulas,
    notas
)
```

Ejemplo:

```
id_alumno: 50
nombre_alumno: Luis Pérez
email: luis@universidad.es
asignaturas: BD, SO, RED
profesores: 10, 14, 22
aulas: B101, A203, C104
notas: 8, 6, 9
```

Dependencias:

```
id_alumno → nombre_alumno, email
id_asignatura → id_profesor, aula
(id_alumno, id_asignatura) → nota
```

### Se pide

1. Llevar la relación a 1FN.
2. Determinar la clave.
3. Eliminar dependencias parciales para obtener 2FN.
4. Eliminar dependencias transitivas para obtener 3FN.
5. Indicar PK y FK.

### Resolución

#### 1. 1FN

```
MATRICULA(
    id_alumno,
    id_asignatura,
    nombre_alumno,
    email,
    id_profesor,
    aula,
    nota
)
```

Clave:

```
PK = (id_alumno, id_asignatura)
```

#### 2. 2FN

```
ALUMNO(
    id_alumno PK,
    nombre_alumno,
    email
)

ASIGNATURA(
    id_asignatura PK,
    id_profesor,
    aula
)

MATRICULA(
    id_alumno PK FK,
    id_asignatura PK FK,
    nota
)
```

#### 3. 3FN

Si además se conoce:

```
id_profesor → nombre_profesor
```

se crea:

```
PROFESOR(
    id_profesor PK,
    nombre_profesor
)

ASIGNATURA(
    id_asignatura PK,
    id_profesor FK,
    aula
)

ALUMNO(
    id_alumno PK,
    nombre_alumno,
    email
)

MATRICULA(
    id_alumno PK FK,
    id_asignatura PK FK,
    nota
)
```

Resultado: 3FN.

