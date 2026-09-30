# Ejercicio 2. Normalización de matrículas universitarias

## Enunciado

Una universidad registra las matrículas de sus estudiantes.

Un estudiante puede matricularse en varias asignaturas y una asignatura puede tener muchos estudiantes. Cada asignatura pertenece a un departamento y cada estudiante puede tener varios teléfonos.

### Modelo Chen

```mermaid
flowchart LR

    EST["ESTUDIANTE"]
    ASI["ASIGNATURA"]
    DEP["DEPARTAMENTO"]

    MAT{"MATRICULA"}
    PERT{"PERTENECE"}

    ID_E(("id_estudiante"))
    NOM_E(("nombre_estudiante"))
    TEL(("telefono"))

    ID_A(("id_asignatura"))
    NOM_A(("nombre_asignatura"))
    CRED(("creditos"))

    ID_D(("id_departamento"))
    NOM_D(("nombre_departamento"))

    CURSO(("curso"))
    NOTA(("nota"))

    EST --- ID_E
    EST --- NOM_E
    EST --- TEL

    ASI --- ID_A
    ASI --- NOM_A
    ASI --- CRED

    DEP --- ID_D
    DEP --- NOM_D

    ASI --- PERT
    PERT --- DEP

    EST --- MAT
    MAT --- ASI
    MAT --- CURSO
    MAT --- NOTA
```

Relación inicial:

```text
MATRICULA(
    id_estudiante,
    nombre_estudiante,
    telefono,
    id_asignatura,
    nombre_asignatura,
    creditos,
    id_departamento,
    nombre_departamento,
    curso,
    nota
)
```

Dependencias funcionales:

```text
id_estudiante → nombre_estudiante
id_asignatura → nombre_asignatura, creditos, id_departamento
id_departamento → nombre_departamento
id_estudiante, id_asignatura, curso → nota
```

Se pide:

1. Identificar el atributo multivaluado.
2. Determinar la clave.
3. Identificar dependencias parciales.
4. Identificar dependencias transitivas.
5. Normalizar hasta 3FN.
6. Indicar las relaciones finales.

## Resolución

### 1. Atributo multivaluado

Un estudiante puede tener varios teléfonos:

```text
telefono
```

Se crea:

```text
TELEFONO_ESTUDIANTE(
    id_estudiante,
    telefono
)
```

Clave:

```text
PK = (id_estudiante, telefono)
```

### 2. Clave de la relación inicial

La nota corresponde a un estudiante, una asignatura y un curso académico:

```text
PK = (id_estudiante, id_asignatura, curso)
```

### 3. Dependencias parciales

Tenemos:

```text
id_estudiante → nombre_estudiante
```

y:

```text
id_asignatura → nombre_asignatura, creditos, id_departamento
```

Ambas dependen solamente de una parte de la clave.

Por tanto, existen dependencias parciales.

La dependencia:

```text
id_estudiante, id_asignatura, curso → nota
```

depende de la clave completa.

### 4. Dependencia transitiva

Tenemos:

```text
id_asignatura → id_departamento
id_departamento → nombre_departamento
```

Por tanto:

```text
id_asignatura → nombre_departamento
```

es una dependencia transitiva.

### 5. Descomposición

#### ESTUDIANTE

```text
ESTUDIANTE(
    id_estudiante PK,
    nombre_estudiante
)
```

#### TELÉFONOS

```text
TELEFONO_ESTUDIANTE(
    id_estudiante PK FK,
    telefono PK
)
```

#### DEPARTAMENTO

```text
DEPARTAMENTO(
    id_departamento PK,
    nombre_departamento
)
```

#### ASIGNATURA

```text
ASIGNATURA(
    id_asignatura PK,
    nombre_asignatura,
    creditos,
    id_departamento FK
)
```

#### MATRÍCULA

```text
MATRICULA(
    id_estudiante PK FK,
    id_asignatura PK FK,
    curso PK,
    nota
)
```

### 6. Resultado final en 3FN

```text
ESTUDIANTE(
    id_estudiante PK,
    nombre_estudiante
)

TELEFONO_ESTUDIANTE(
    id_estudiante PK FK,
    telefono PK
)

DEPARTAMENTO(
    id_departamento PK,
    nombre_departamento
)

ASIGNATURA(
    id_asignatura PK,
    nombre_asignatura,
    creditos,
    id_departamento FK
)

MATRICULA(
    id_estudiante PK FK,
    id_asignatura PK FK,
    curso PK,
    nota
)
```

### 7. Dependencias finales

```text
ESTUDIANTE
id_estudiante → nombre_estudiante

DEPARTAMENTO
id_departamento → nombre_departamento

ASIGNATURA
id_asignatura → nombre_asignatura, creditos, id_departamento

MATRICULA
id_estudiante, id_asignatura, curso → nota

TELEFONO_ESTUDIANTE
id_estudiante, telefono → ninguno
```

Resultado: no quedan dependencias parciales ni transitivas en las relaciones resultantes.

### 8. Diagrama Relacional

```mermaid
erDiagram

    DEPARTAMENTO ||--o{ ASIGNATURA : "ofrece"
    ESTUDIANTE ||--o{ TELEFONO_ESTUDIANTE : "tiene"
    ESTUDIANTE ||--o{ MATRICULA : "realiza"
    ASIGNATURA ||--o{ MATRICULA : "recibe"

    ESTUDIANTE {
        INT id_estudiante PK "NOT NULL"
        VARCHAR nombre_estudiante "NOT NULL"
    }

    TELEFONO_ESTUDIANTE {
        INT id_estudiante PK, FK "NOT NULL"
        VARCHAR telefono PK "NOT NULL"
    }

    DEPARTAMENTO {
        INT id_departamento PK "NOT NULL"
        VARCHAR nombre_departamento "NOT NULL, UNIQUE"
    }

    ASIGNATURA {
        INT id_asignatura PK "NOT NULL"
        VARCHAR nombre_asignatura "NOT NULL, UNIQUE"
        INT creditos "NOT NULL, CHECK creditos > 0"
        INT id_departamento FK "NOT NULL"
    }

    MATRICULA {
        INT id_estudiante PK, FK "NOT NULL"
        INT id_asignatura PK, FK "NOT NULL"
        VARCHAR curso PK "NOT NULL"
        DECIMAL nota "NULL, CHECK nota >= 0 AND nota <= 10"
    }
```

### Restricciones

```text
ESTUDIANTE
PK: id_estudiante
NOT NULL: todos los atributos

TELEFONO_ESTUDIANTE
PK: (id_estudiante, telefono)
FK: id_estudiante → ESTUDIANTE(id_estudiante)
NOT NULL: todos los atributos

DEPARTAMENTO
PK: id_departamento
UNIQUE: nombre_departamento
NOT NULL: todos los atributos

ASIGNATURA
PK: id_asignatura
FK: id_departamento → DEPARTAMENTO(id_departamento)
UNIQUE: nombre_asignatura
CHECK: creditos > 0
NOT NULL: todos los atributos

MATRICULA
PK: (id_estudiante, id_asignatura, curso)
FK: id_estudiante → ESTUDIANTE(id_estudiante)
FK: id_asignatura → ASIGNATURA(id_asignatura)
NOT NULL: id_estudiante, id_asignatura, curso
NULL: nota
CHECK: nota >= 0 AND nota <= 10 cuando nota no sea NULL
```

`nota` es nullable porque una matrícula puede existir antes de que el estudiante haya recibido una calificación.

