# Del modelo Chen a relaciones normalizadas

## Ejercicio 1. Biblioteca

### Enunciado

A partir del siguiente modelo Chen, obtén directamente las relaciones necesarias.

```mermaid
flowchart LR

    SOC["SOCIO"]
    LIB["LIBRO"]
    AUT["AUTOR"]
    EJ["EJEMPLAR"]
    PRE["PRESTAMO"]

    ESCRIBE{"ESCRIBE"}
    TIENE{"TIENE"}
    REALIZA{"REALIZA"}
    AFECTA{"AFECTA"}

    ID_S(("id_socio"))
    NOM_S(("nombre"))
    TEL(("telefono"))

    ID_L(("id_libro"))
    TIT(("titulo"))
    ISBN(("isbn"))

    ID_A(("id_autor"))
    NOM_A(("nombre"))

    ID_E(("id_ejemplar"))
    EST(("estado"))

    ID_P(("id_prestamo"))
    F_PRE(("fecha_prestamo"))
    F_DEV(("fecha_devolucion"))

    SOC --- ID_S
    SOC --- NOM_S
    SOC --- TEL

    LIB --- ID_L
    LIB --- TIT
    LIB --- ISBN

    AUT --- ID_A
    AUT --- NOM_A

    EJ --- ID_E
    EJ --- EST

    PRE --- ID_P
    PRE --- F_PRE
    PRE --- F_DEV

    AUT --- ESCRIBE
    ESCRIBE --- LIB

    LIB --- TIENE
    TIENE --- EJ

    SOC --- REALIZA
    REALIZA --- PRE

    PRE --- AFECTA
    AFECTA --- EJ
```

### Se pide

1. Transformar las entidades fuertes en relaciones.
2. Transformar las relaciones 1 y N.
3. Detectar el atributo multivaluado.
4. Determinar si alguna relación necesita transformación adicional para alcanzar 1FN, 2FN o 3FN.
5. Obtener el esquema final.

### Resolución

```
SOCIO(
    id_socio PK,
    nombre
)

TELEFONO_SOCIO(
    id_socio PK FK,
    telefono PK
)

LIBRO(
    id_libro PK,
    titulo,
    isbn UNIQUE
)

AUTOR(
    id_autor PK,
    nombre
)

ESCRIBE(
    id_autor PK FK,
    id_libro PK FK
)

EJEMPLAR(
    id_ejemplar PK,
    estado,
    id_libro FK
)

PRESTAMO(
    id_prestamo PK,
    fecha_prestamo,
    fecha_devolucion,
    id_socio FK,
    id_ejemplar FK
)
```

Todas las relaciones obtenidas cumplen 1FN.

Las relaciones con clave compuesta:

```
ESCRIBE
TELEFONO_SOCIO
```

no presentan atributos no clave, por lo que no introducen dependencias parciales.

No aparecen dependencias transitivas dentro de las relaciones resultantes.

Por tanto, el diseño se encuentra en 3FN.

### Diagrama relacional final

```mermaid
erDiagram

    SOCIO ||--o{ TELEFONO_SOCIO : "tiene"
    SOCIO ||--o{ PRESTAMO : "realiza"
    LIBRO ||--o{ EJEMPLAR : "tiene"
    EJEMPLAR ||--o{ PRESTAMO : "es_prestado"
    AUTOR ||--o{ ESCRIBE : "escribe"
    LIBRO ||--o{ ESCRIBE : "tiene"

    SOCIO {
        INT id_socio PK "NOT NULL"
        VARCHAR nombre "NOT NULL"
    }

    TELEFONO_SOCIO {
        INT id_socio PK, FK "NOT NULL"
        VARCHAR telefono PK "NOT NULL"
    }

    LIBRO {
        INT id_libro PK "NOT NULL"
        VARCHAR titulo "NOT NULL"
        VARCHAR isbn "NOT NULL, UNIQUE"
    }

    AUTOR {
        INT id_autor PK "NOT NULL"
        VARCHAR nombre "NOT NULL"
    }

    ESCRIBE {
        INT id_autor PK, FK "NOT NULL"
        INT id_libro PK, FK "NOT NULL"
    }

    EJEMPLAR {
        INT id_ejemplar PK "NOT NULL"
        VARCHAR estado "NOT NULL"
        INT id_libro FK "NOT NULL"
    }

    PRESTAMO {
        INT id_prestamo PK "NOT NULL"
        DATE fecha_prestamo "NOT NULL"
        DATE fecha_devolucion "NULL"
        INT id_socio FK "NOT NULL"
        INT id_ejemplar FK "NOT NULL"
    }
```

## Ejercicio 2. Clínica veterinaria

### Enunciado

A partir del siguiente modelo Chen:

```mermaid
flowchart LR

    CLI["CLIENTE"]
    MAS["MASCOTA"]
    VET["VETERINARIO"]
    ESP["ESPECIALIDAD"]
    CON["CONSULTA"]
    MED["MEDICAMENTO"]

    TIENE{"TIENE"}
    ATIENDE{"ATIENDE"}
    POSEE{"POSEE"}
    UTILIZA{"UTILIZA"}
    PERTENECE{"PERTENECE"}

    ID_C(("id_cliente"))
    NOM_C(("nombre"))
    TEL(("telefono"))

    ID_M(("id_mascota"))
    NOM_M(("nombre"))
    ESPECIE(("especie"))

    ID_V(("id_veterinario"))
    NOM_V(("nombre"))

    ID_E(("id_especialidad"))
    NOM_E(("nombre"))

    ID_CO(("id_consulta"))
    FECHA(("fecha"))
    DIAG(("diagnostico"))

    ID_MED(("id_medicamento"))
    NOM_MED(("nombre"))
    DOSIS(("dosis"))

    CLI --- ID_C
    CLI --- NOM_C
    CLI --- TEL

    MAS --- ID_M
    MAS --- NOM_M
    MAS --- ESPECIE

    VET --- ID_V
    VET --- NOM_V

    ESP --- ID_E
    ESP --- NOM_E

    CON --- ID_CO
    CON --- FECHA
    CON --- DIAG

    MED --- ID_MED
    MED --- NOM_MED
    MED --- DOSIS

    CLI --- TIENE
    TIENE --- MAS

    VET --- ATIENDE
    ATIENDE --- CON

    MAS --- POSEE
    POSEE --- CON

    VET --- PERTENECE
    PERTENECE --- ESP

    CON --- UTILIZA
    UTILIZA --- MED
```

### Se pide

1. Transformar las entidades fuertes en relaciones.
2. Transformar las relaciones 1.
3. Transformar las relaciones N.
4. Detectar el atributo multivaluado.
5. Determinar si las relaciones obtenidas están en 1FN.
6. Comprobar 2FN cuando exista una clave compuesta.
7. Comprobar 3FN.
8. Obtener el modelo relacional final.

### Resolución

```
CLIENTE(
    id_cliente PK,
    nombre
)

TELEFONO_CLIENTE(
    id_cliente PK FK,
    telefono PK
)

MASCOTA(
    id_mascota PK,
    nombre,
    especie,
    id_cliente FK
)

VETERINARIO(
    id_veterinario PK,
    nombre,
    id_especialidad FK
)

ESPECIALIDAD(
    id_especialidad PK,
    nombre
)

CONSULTA(
    id_consulta PK,
    fecha,
    diagnostico,
    id_veterinario FK,
    id_mascota FK
)

MEDICAMENTO(
    id_medicamento PK,
    nombre
)

UTILIZA(
    id_consulta PK FK,
    id_medicamento PK FK,
    dosis
)
```

### Comprobación de normalización

`<span>telefono</span>` es multivaluado, por lo que se crea:

```
TELEFONO_CLIENTE(
    id_cliente PK FK,
    telefono PK
)
```

La relación `<span>UTILIZA</span>` tiene clave compuesta:

```
(id_consulta, id_medicamento)
```

y `<span>dosis</span>` depende de la clave completa:

```
(id_consulta, id_medicamento) → dosis
```

Por tanto no existe dependencia parcial.

Las claves foráneas:

```
id_cliente
id_veterinario
id_mascota
id_especialidad
```

no generan dependencias transitivas dentro de sus propias relaciones.

El esquema final queda en 3FN.

### Diagrama relacional final

```mermaid
erDiagram

    CLIENTE ||--o{ TELEFONO_CLIENTE : "tiene"
    CLIENTE ||--o{ MASCOTA : "posee"
    ESPECIALIDAD ||--o{ VETERINARIO : "incluye"
    VETERINARIO ||--o{ CONSULTA : "atiende"
    MASCOTA ||--o{ CONSULTA : "recibe"
    CONSULTA ||--o{ UTILIZA : "utiliza"
    MEDICAMENTO ||--o{ UTILIZA : "aparece"

    CLIENTE {
        INT id_cliente PK "NOT NULL"
        VARCHAR nombre "NOT NULL"
    }

    TELEFONO_CLIENTE {
        INT id_cliente PK, FK "NOT NULL"
        VARCHAR telefono PK "NOT NULL"
    }

    MASCOTA {
        INT id_mascota PK "NOT NULL"
        VARCHAR nombre "NOT NULL"
        VARCHAR especie "NOT NULL"
        INT id_cliente FK "NOT NULL"
    }

    ESPECIALIDAD {
        INT id_especialidad PK "NOT NULL"
        VARCHAR nombre "NOT NULL, UNIQUE"
    }

    VETERINARIO {
        INT id_veterinario PK "NOT NULL"
        VARCHAR nombre "NOT NULL"
        INT id_especialidad FK "NOT NULL"
    }

    CONSULTA {
        INT id_consulta PK "NOT NULL"
        DATE fecha "NOT NULL"
        VARCHAR diagnostico "NULL"
        INT id_veterinario FK "NOT NULL"
        INT id_mascota FK "NOT NULL"
    }

    MEDICAMENTO {
        INT id_medicamento PK "NOT NULL"
        VARCHAR nombre "NOT NULL, UNIQUE"
    }

    UTILIZA {
        INT id_consulta PK, FK "NOT NULL"
        INT id_medicamento PK, FK "NOT NULL"
        VARCHAR dosis "NOT NULL"
    }
```

