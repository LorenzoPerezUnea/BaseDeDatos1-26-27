# V1 - UNIVERSIDAD

## Modelo relacional inicial

### ESTUDIANTE

| Atributo       | Tipo de dato | Restricciones    |
| ---------------- | -------------- | ------------------ |
| id\_estudiante | INT          | PK, NOT NULL     |
| nombre         | VARCHAR(100) | NOT NULL         |
| correo         | VARCHAR(150) | UNIQUE, NOT NULL |

### ESTUDIANTE\_TELEFONO

| Atributo       | Tipo de dato | Restricciones                                  |
| ---------------- | -------------- | ------------------------------------------------ |
| id\_estudiante | INT          | PK, FK -> ESTUDIANTE(id\_estudiante), NOT NULL |
| telefono       | VARCHAR(20)  | PK, NOT NULL                                   |

### TITULACION

| Atributo           | Tipo de dato | Restricciones |
| -------------------- | -------------- | --------------- |
| nombre\_titulacion | VARCHAR(100) | PK, NOT NULL  |

### ASIGNATURA

| Atributo           | Tipo de dato | Restricciones                                  |
| -------------------- | -------------- | ------------------------------------------------ |
| id\_asignatura     | INT          | PK, NOT NULL                                   |
| nombre             | VARCHAR(100) | NOT NULL                                       |
| nombre\_titulacion | VARCHAR(100) | FK -> TITULACION(nombre\_titulacion), NOT NULL |

### PROFESOR

| Atributo     | Tipo de dato | Restricciones    |
| -------------- | -------------- | ------------------ |
| id\_profesor | INT          | PK, NOT NULL     |
| nombre       | VARCHAR(100) | NOT NULL         |
| correo       | VARCHAR(150) | UNIQUE, NOT NULL |

> La clave compuesta supone una única matrícula por estudiante y asignatura. Si se permiten repeticiones en distintos cursos académicos, la clave debe incorporar ese contexto o un identificador de matrícula.

### MATRICULA

| Atributo       | Tipo de dato | Restricciones                                  |
| ---------------- | -------------- | ------------------------------------------------ |
| id\_estudiante | INT          | PK, FK -> ESTUDIANTE(id\_estudiante), NOT NULL |
| id\_asignatura | INT          | PK, FK -> ASIGNATURA(id\_asignatura), NOT NULL |
| fecha          | DATE         | NOT NULL                                       |
| calificacion   | DECIMAL(4,2) | NULL                                           |

### IMPARTE

| Atributo       | Tipo de dato | Restricciones                                  |
| ---------------- | -------------- | ------------------------------------------------ |
| id\_profesor   | INT          | PK, FK -> PROFESOR(id\_profesor), NOT NULL     |
| id\_asignatura | INT          | PK, FK -> ASIGNATURA(id\_asignatura), NOT NULL |

## Primera Forma Normal (1FN)

### Descomposición de ESTUDIANTE

### ESTUDIANTE

| Atributo       | Tipo de dato | Restricciones    |
| ---------------- | -------------- | ------------------ |
| id\_estudiante | INT          | PK, NOT NULL     |
| nombre         | VARCHAR(100) | NOT NULL         |
| correo         | VARCHAR(150) | UNIQUE, NOT NULL |

### ESTUDIANTE\_TELEFONO

| Atributo       | Tipo de dato | Restricciones                                  |
| ---------------- | -------------- | ------------------------------------------------ |
| id\_estudiante | INT          | PK, FK -> ESTUDIANTE(id\_estudiante), NOT NULL |
| telefono       | VARCHAR(20)  | PK, NOT NULL                                   |

## Segunda Forma Normal (2FN)

### MATRICULA

| Atributo       | Tipo de dato | Restricciones                                  |
| ---------------- | -------------- | ------------------------------------------------ |
| id\_estudiante | INT          | PK, FK -> ESTUDIANTE(id\_estudiante), NOT NULL |
| id\_asignatura | INT          | PK, FK -> ASIGNATURA(id\_asignatura), NOT NULL |
| fecha          | DATE         | NOT NULL                                       |
| calificacion   | DECIMAL(4,2) | NULL                                           |

## Tercera Forma Normal (3FN)

### ASIGNATURA

| Atributo           | Tipo de dato | Restricciones                                  |
| -------------------- | -------------- | ------------------------------------------------ |
| id\_asignatura     | INT          | PK, NOT NULL                                   |
| nombre             | VARCHAR(100) | NOT NULL                                       |
| nombre\_titulacion | VARCHAR(100) | FK -> TITULACION(nombre\_titulacion), NOT NULL |

### TITULACION

| Atributo           | Tipo de dato | Restricciones |
| -------------------- | -------------- | --------------- |
| nombre\_titulacion | VARCHAR(100) | PK, NOT NULL  |

## Diagrama relacional final

```mermaid
erDiagram
    ESTUDIANTE {
        INT id_estudiante PK
        VARCHAR nombre
        VARCHAR correo UK
    }

    ESTUDIANTE_TELEFONO {
        INT id_estudiante PK, FK
        VARCHAR telefono PK
    }

    TITULACION {
        VARCHAR nombre_titulacion PK
    }

    ASIGNATURA {
        INT id_asignatura PK
        VARCHAR nombre
        VARCHAR nombre_titulacion FK
    }

    PROFESOR {
        INT id_profesor PK
        VARCHAR nombre
        VARCHAR correo UK
    }

    MATRICULA {
        INT id_estudiante PK, FK
        INT id_asignatura PK, FK
        DATE fecha
        DECIMAL calificacion
    }

    IMPARTE {
        INT id_profesor PK, FK
        INT id_asignatura PK, FK
    }

    ESTUDIANTE ||--o{ ESTUDIANTE_TELEFONO : tiene
    ESTUDIANTE ||--o{ MATRICULA : realiza
    ASIGNATURA ||--o{ MATRICULA : recibe
    TITULACION ||--o{ ASIGNATURA : incluye
    PROFESOR ||--o{ IMPARTE : participa
    ASIGNATURA ||--o{ IMPARTE : recibe
```

# V2 - BIBLIOTECA

## Modelo relacional inicial

### SOCIO

| Atributo  | Tipo de dato | Restricciones    |
| ----------- | -------------- | ------------------ |
| id\_socio | INT          | PK, NOT NULL     |
| nombre    | VARCHAR(100) | NOT NULL         |
| correo    | VARCHAR(150) | UNIQUE, NOT NULL |

### SOCIO\_TELEFONO

| Atributo  | Tipo de dato | Restricciones                        |
| ----------- | -------------- | -------------------------------------- |
| id\_socio | INT          | PK, FK -> SOCIO(id\_socio), NOT NULL |
| telefono  | VARCHAR(20)  | PK, NOT NULL                         |

### EDITORIAL

| Atributo          | Tipo de dato | Restricciones |
| ------------------- | -------------- | --------------- |
| id\_editorial     | INT          | PK, NOT NULL  |
| nombre\_editorial | VARCHAR(150) | NOT NULL      |
| pais              | VARCHAR(100) | NOT NULL      |

### LIBRO

| Atributo      | Tipo de dato | Restricciones                            |
| --------------- | -------------- | ------------------------------------------ |
| ISBN          | VARCHAR(20)  | PK, NOT NULL                             |
| titulo        | VARCHAR(200) | NOT NULL                                 |
| id\_editorial | INT          | FK -> EDITORIAL(id\_editorial), NOT NULL |

### AUTOR

| Atributo      | Tipo de dato | Restricciones |
| --------------- | -------------- | --------------- |
| id\_autor     | INT          | PK, NOT NULL  |
| nombre\_autor | VARCHAR(150) | NOT NULL      |

### LIBRO\_AUTOR

| Atributo  | Tipo de dato | Restricciones                        |
| ----------- | -------------- | -------------------------------------- |
| ISBN      | VARCHAR(20)  | PK, FK -> LIBRO(ISBN), NOT NULL      |
| id\_autor | INT          | PK, FK -> AUTOR(id\_autor), NOT NULL |

### PRESTAMO

| Atributo        | Tipo de dato | Restricciones                    |
| ----------------- | -------------- | ---------------------------------- |
| id\_prestamo    | INT          | PK, NOT NULL                     |
| id\_socio       | INT          | FK -> SOCIO(id\_socio), NOT NULL |
| ISBN            | VARCHAR(20)  | FK -> LIBRO(ISBN), NOT NULL      |
| fecha\_prestamo | DATE         | NOT NULL                         |
| fecha\_prevista | DATE         | NOT NULL                         |
| fecha\_real     | DATE         | NULL                             |

## Primera Forma Normal (1FN)

### SOCIO

| Atributo  | Tipo de dato | Restricciones    |
| ----------- | -------------- | ------------------ |
| id\_socio | INT          | PK, NOT NULL     |
| nombre    | VARCHAR(100) | NOT NULL         |
| correo    | VARCHAR(150) | UNIQUE, NOT NULL |

### SOCIO\_TELEFONO

| Atributo  | Tipo de dato | Restricciones                        |
| ----------- | -------------- | -------------------------------------- |
| id\_socio | INT          | PK, FK -> SOCIO(id\_socio), NOT NULL |
| telefono  | VARCHAR(20)  | PK, NOT NULL                         |

## Segunda Forma Normal (2FN)

### LIBRO\_AUTOR

| Atributo  | Tipo de dato | Restricciones                        |
| ----------- | -------------- | -------------------------------------- |
| ISBN      | VARCHAR(20)  | PK, FK -> LIBRO(ISBN), NOT NULL      |
| id\_autor | INT          | PK, FK -> AUTOR(id\_autor), NOT NULL |

## Tercera Forma Normal (3FN)

### LIBRO

| Atributo      | Tipo de dato | Restricciones                            |
| --------------- | -------------- | ------------------------------------------ |
| ISBN          | VARCHAR(20)  | PK, NOT NULL                             |
| titulo        | VARCHAR(200) | NOT NULL                                 |
| id\_editorial | INT          | FK -> EDITORIAL(id\_editorial), NOT NULL |

### EDITORIAL

| Atributo          | Tipo de dato | Restricciones |
| ------------------- | -------------- | --------------- |
| id\_editorial     | INT          | PK, NOT NULL  |
| nombre\_editorial | VARCHAR(150) | NOT NULL      |
| pais              | VARCHAR(100) | NOT NULL      |

## Diagrama relacional final

```mermaid
erDiagram
    SOCIO {
        INT id_socio PK
        VARCHAR nombre
        VARCHAR correo UK
    }

    SOCIO_TELEFONO {
        INT id_socio PK, FK
        VARCHAR telefono PK
    }

    EDITORIAL {
        INT id_editorial PK
        VARCHAR nombre_editorial
        VARCHAR pais
    }

    LIBRO {
        VARCHAR ISBN PK
        VARCHAR titulo
        INT id_editorial FK
    }

    AUTOR {
        INT id_autor PK
        VARCHAR nombre_autor
    }

    LIBRO_AUTOR {
        VARCHAR ISBN PK, FK
        INT id_autor PK, FK
    }

    PRESTAMO {
        INT id_prestamo PK
        INT id_socio FK
        VARCHAR ISBN FK
        DATE fecha_prestamo
        DATE fecha_prevista
        DATE fecha_real
    }

    SOCIO ||--o{ SOCIO_TELEFONO : tiene
    EDITORIAL ||--o{ LIBRO : publica
    LIBRO ||--o{ LIBRO_AUTOR : relaciona
    AUTOR ||--o{ LIBRO_AUTOR : escribe
    SOCIO ||--o{ PRESTAMO : realiza
    LIBRO ||--o{ PRESTAMO : recibe
```

# V3 - CLINICA

## Modelo relacional inicial

### PACIENTE

| Atributo          | Tipo de dato | Restricciones |
| ------------------- | -------------- | --------------- |
| id\_paciente      | INT          | PK, NOT NULL  |
| nombre            | VARCHAR(100) | NOT NULL      |
| fecha\_nacimiento | DATE         | NOT NULL      |

### PACIENTE\_TELEFONO

| Atributo     | Tipo de dato | Restricciones                              |
| -------------- | -------------- | -------------------------------------------- |
| id\_paciente | INT          | PK, FK -> PACIENTE(id\_paciente), NOT NULL |
| telefono     | VARCHAR(20)  | PK, NOT NULL                               |

### ESPECIALIDAD

| Atributo             | Tipo de dato | Restricciones |
| ---------------------- | -------------- | --------------- |
| id\_especialidad     | INT          | PK, NOT NULL  |
| nombre\_especialidad | VARCHAR(100) | NOT NULL      |

### MEDICO

| Atributo         | Tipo de dato | Restricciones                                  |
| ------------------ | -------------- | ------------------------------------------------ |
| id\_medico       | INT          | PK, NOT NULL                                   |
| nombre           | VARCHAR(100) | NOT NULL                                       |
| id\_especialidad | INT          | FK -> ESPECIALIDAD(id\_especialidad), NOT NULL |

### CONSULTA

| Atributo     | Tipo de dato | Restricciones                          |
| -------------- | -------------- | ---------------------------------------- |
| id\_consulta | INT          | PK, NOT NULL                           |
| id\_paciente | INT          | FK -> PACIENTE(id\_paciente), NOT NULL |
| id\_medico   | INT          | FK -> MEDICO(id\_medico), NOT NULL     |
| fecha        | DATETIME     | NOT NULL                               |
| motivo       | VARCHAR(250) | NOT NULL                               |
| diagnostico  | TEXT         | NULL                                   |

### TRATAMIENTO

| Atributo        | Tipo de dato | Restricciones |
| ----------------- | -------------- | --------------- |
| id\_tratamiento | INT          | PK, NOT NULL  |
| descripcion     | VARCHAR(250) | NOT NULL      |

### CONSULTA\_TRATAMIENTO

| Atributo        | Tipo de dato | Restricciones                                    |
| ----------------- | -------------- | -------------------------------------------------- |
| id\_consulta    | INT          | PK, FK -> CONSULTA(id\_consulta), NOT NULL       |
| id\_tratamiento | INT          | PK, FK -> TRATAMIENTO(id\_tratamiento), NOT NULL |
| dosis           | VARCHAR(100) | NOT NULL                                         |

## Primera Forma Normal (1FN)

### PACIENTE

| Atributo          | Tipo de dato | Restricciones |
| ------------------- | -------------- | --------------- |
| id\_paciente      | INT          | PK, NOT NULL  |
| nombre            | VARCHAR(100) | NOT NULL      |
| fecha\_nacimiento | DATE         | NOT NULL      |

### PACIENTE\_TELEFONO

| Atributo     | Tipo de dato | Restricciones                              |
| -------------- | -------------- | -------------------------------------------- |
| id\_paciente | INT          | PK, FK -> PACIENTE(id\_paciente), NOT NULL |
| telefono     | VARCHAR(20)  | PK, NOT NULL                               |

## Segunda Forma Normal (2FN)

### CONSULTA\_TRATAMIENTO

| Atributo        | Tipo de dato | Restricciones                                    |
| ----------------- | -------------- | -------------------------------------------------- |
| id\_consulta    | INT          | PK, FK -> CONSULTA(id\_consulta), NOT NULL       |
| id\_tratamiento | INT          | PK, FK -> TRATAMIENTO(id\_tratamiento), NOT NULL |
| dosis           | VARCHAR(100) | NOT NULL                                         |

## Tercera Forma Normal (3FN)

### MEDICO

| Atributo         | Tipo de dato | Restricciones                                  |
| ------------------ | -------------- | ------------------------------------------------ |
| id\_medico       | INT          | PK, NOT NULL                                   |
| nombre           | VARCHAR(100) | NOT NULL                                       |
| id\_especialidad | INT          | FK -> ESPECIALIDAD(id\_especialidad), NOT NULL |

### ESPECIALIDAD

| Atributo             | Tipo de dato | Restricciones |
| ---------------------- | -------------- | --------------- |
| id\_especialidad     | INT          | PK, NOT NULL  |
| nombre\_especialidad | VARCHAR(100) | NOT NULL      |

## Diagrama relacional final

```mermaid
erDiagram
    PACIENTE {
        INT id_paciente PK
        VARCHAR nombre
        DATE fecha_nacimiento
    }

    PACIENTE_TELEFONO {
        INT id_paciente PK, FK
        VARCHAR telefono PK
    }

    ESPECIALIDAD {
        INT id_especialidad PK
        VARCHAR nombre_especialidad
    }

    MEDICO {
        INT id_medico PK
        VARCHAR nombre
        INT id_especialidad FK
    }

    CONSULTA {
        INT id_consulta PK
        INT id_paciente FK
        INT id_medico FK
        DATETIME fecha
        VARCHAR motivo
        TEXT diagnostico
    }

    TRATAMIENTO {
        INT id_tratamiento PK
        VARCHAR descripcion
    }

    CONSULTA_TRATAMIENTO {
        INT id_consulta PK, FK
        INT id_tratamiento PK, FK
        VARCHAR dosis
    }

    PACIENTE ||--o{ PACIENTE_TELEFONO : tiene
    PACIENTE ||--o{ CONSULTA : realiza
    MEDICO ||--o{ CONSULTA : atiende
    ESPECIALIDAD ||--o{ MEDICO : agrupa
    CONSULTA ||--o{ CONSULTA_TRATAMIENTO : incluye
    TRATAMIENTO ||--o{ CONSULTA_TRATAMIENTO : aparece
```

# V4 - TIENDA EN LINEA

## Modelo relacional inicial

### CLIENTE

| Atributo    | Tipo de dato | Restricciones    |
| ------------- | -------------- | ------------------ |
| id\_cliente | INT          | PK, NOT NULL     |
| nombre      | VARCHAR(100) | NOT NULL         |
| correo      | VARCHAR(150) | UNIQUE, NOT NULL |

### CLIENTE\_DIRECCION

| Atributo    | Tipo de dato | Restricciones                            |
| ------------- | -------------- | ------------------------------------------ |
| id\_cliente | INT          | PK, FK -> CLIENTE(id\_cliente), NOT NULL |
| direccion   | VARCHAR(250) | PK, NOT NULL                             |

### PEDIDO

| Atributo    | Tipo de dato | Restricciones                        |
| ------------- | -------------- | -------------------------------------- |
| id\_pedido  | INT          | PK, NOT NULL                         |
| fecha       | DATETIME     | NOT NULL                             |
| id\_cliente | INT          | FK -> CLIENTE(id\_cliente), NOT NULL |

### CATEGORIA

| Atributo          | Tipo de dato | Restricciones |
| ------------------- | -------------- | --------------- |
| id\_categoria     | INT          | PK, NOT NULL  |
| nombre\_categoria | VARCHAR(100) | NOT NULL      |

### PRODUCTO

| Atributo         | Tipo de dato | Restricciones                            |
| ------------------ | -------------- | ------------------------------------------ |
| id\_producto     | INT          | PK, NOT NULL                             |
| nombre\_producto | VARCHAR(150) | NOT NULL                                 |
| id\_categoria    | INT          | FK -> CATEGORIA(id\_categoria), NOT NULL |

### PROVEEDOR

| Atributo      | Tipo de dato | Restricciones |
| --------------- | -------------- | --------------- |
| id\_proveedor | INT          | PK, NOT NULL  |
| razon\_social | VARCHAR(200) | NOT NULL      |

> La clave compuesta supone una sola línea por producto dentro de cada pedido. Si se permiten varias líneas del mismo producto en un pedido, debe añadirse un identificador de línea o redefinirse la clave.

### DETALLE\_PEDIDO

| Atributo                   | Tipo de dato  | Restricciones                              |
| ---------------------------- | --------------- | -------------------------------------------- |
| id\_pedido                 | INT           | PK, FK -> PEDIDO(id\_pedido), NOT NULL     |
| id\_producto               | INT           | PK, FK -> PRODUCTO(id\_producto), NOT NULL |
| cantidad                   | INT           | NOT NULL                                   |
| precio\_unitario\_aplicado | DECIMAL(10,2) | NOT NULL                                   |

### PRODUCTO\_PROVEEDOR

| Atributo      | Tipo de dato | Restricciones                                |
| --------------- | -------------- | ---------------------------------------------- |
| id\_producto  | INT          | PK, FK -> PRODUCTO(id\_producto), NOT NULL   |
| id\_proveedor | INT          | PK, FK -> PROVEEDOR(id\_proveedor), NOT NULL |

## Primera Forma Normal (1FN)

### CLIENTE

| Atributo    | Tipo de dato | Restricciones    |
| ------------- | -------------- | ------------------ |
| id\_cliente | INT          | PK, NOT NULL     |
| nombre      | VARCHAR(100) | NOT NULL         |
| correo      | VARCHAR(150) | UNIQUE, NOT NULL |

### CLIENTE\_DIRECCION

| Atributo    | Tipo de dato | Restricciones                            |
| ------------- | -------------- | ------------------------------------------ |
| id\_cliente | INT          | PK, FK -> CLIENTE(id\_cliente), NOT NULL |
| direccion   | VARCHAR(250) | PK, NOT NULL                             |

## Segunda Forma Normal (2FN)

### DETALLE\_PEDIDO

| Atributo                   | Tipo de dato  | Restricciones                              |
| ---------------------------- | --------------- | -------------------------------------------- |
| id\_pedido                 | INT           | PK, FK -> PEDIDO(id\_pedido), NOT NULL     |
| id\_producto               | INT           | PK, FK -> PRODUCTO(id\_producto), NOT NULL |
| cantidad                   | INT           | NOT NULL                                   |
| precio\_unitario\_aplicado | DECIMAL(10,2) | NOT NULL                                   |

## Tercera Forma Normal (3FN)

### PRODUCTO

| Atributo         | Tipo de dato | Restricciones                            |
| ------------------ | -------------- | ------------------------------------------ |
| id\_producto     | INT          | PK, NOT NULL                             |
| nombre\_producto | VARCHAR(150) | NOT NULL                                 |
| id\_categoria    | INT          | FK -> CATEGORIA(id\_categoria), NOT NULL |

### CATEGORIA

| Atributo          | Tipo de dato | Restricciones |
| ------------------- | -------------- | --------------- |
| id\_categoria     | INT          | PK, NOT NULL  |
| nombre\_categoria | VARCHAR(100) | NOT NULL      |

## Diagrama relacional final

```mermaid
erDiagram
    CLIENTE {
        INT id_cliente PK
        VARCHAR nombre
        VARCHAR correo UK
    }

    CLIENTE_DIRECCION {
        INT id_cliente PK, FK
        VARCHAR direccion PK
    }

    PEDIDO {
        INT id_pedido PK
        DATETIME fecha
        INT id_cliente FK
    }

    CATEGORIA {
        INT id_categoria PK
        VARCHAR nombre_categoria
    }

    PRODUCTO {
        INT id_producto PK
        VARCHAR nombre_producto
        INT id_categoria FK
    }

    PROVEEDOR {
        INT id_proveedor PK
        VARCHAR razon_social
    }

    DETALLE_PEDIDO {
        INT id_pedido PK, FK
        INT id_producto PK, FK
        INT cantidad
        DECIMAL precio_unitario_aplicado
    }

    PRODUCTO_PROVEEDOR {
        INT id_producto PK, FK
        INT id_proveedor PK, FK
    }

    CLIENTE ||--o{ CLIENTE_DIRECCION : registra
    CLIENTE ||--o{ PEDIDO : realiza
    PEDIDO ||--o{ DETALLE_PEDIDO : contiene
    PRODUCTO ||--o{ DETALLE_PEDIDO : aparece
    CATEGORIA ||--o{ PRODUCTO : clasifica
    PRODUCTO ||--o{ PRODUCTO_PROVEEDOR : relaciona
    PROVEEDOR ||--o{ PRODUCTO_PROVEEDOR : suministra
```

# V5 - ALQUILER DE VEHÍCULOS

## Modelo relacional inicial

### CLIENTE

| Atributo    | Tipo de dato | Restricciones    |
| ------------- | -------------- | ------------------ |
| id\_cliente | INT          | PK, NOT NULL     |
| nombre      | VARCHAR(100) | NOT NULL         |
| correo      | VARCHAR(150) | UNIQUE, NOT NULL |

### CLIENTE\_TELEFONO

| Atributo    | Tipo de dato | Restricciones                            |
| ------------- | -------------- | ------------------------------------------ |
| id\_cliente | INT          | PK, FK -> CLIENTE(id\_cliente), NOT NULL |
| telefono    | VARCHAR(20)  | PK, NOT NULL                             |

### OFICINA

| Atributo    | Tipo de dato | Restricciones |
| ------------- | -------------- | --------------- |
| id\_oficina | INT          | PK, NOT NULL  |

### TIPO\_VEHICULO

| Atributo          | Tipo de dato  | Restricciones |
| ------------------- | --------------- | --------------- |
| id\_tipo          | INT           | PK, NOT NULL  |
| descripcion\_tipo | VARCHAR(100)  | NOT NULL      |
| tarifa\_base      | DECIMAL(10,2) | NOT NULL      |

### VEHICULO

| Atributo    | Tipo de dato | Restricciones                            |
| ------------- | -------------- | ------------------------------------------ |
| matricula   | VARCHAR(15)  | PK, NOT NULL                             |
| modelo      | VARCHAR(100) | NOT NULL                                 |
| id\_tipo    | INT          | FK -> TIPO\_VEHICULO(id\_tipo), NOT NULL |
| id\_oficina | INT          | FK -> OFICINA(id\_oficina), NOT NULL     |

### ALQUILER

| Atributo      | Tipo de dato | Restricciones                        |
| --------------- | -------------- | -------------------------------------- |
| id\_alquiler  | INT          | PK, NOT NULL                         |
| id\_cliente   | INT          | FK -> CLIENTE(id\_cliente), NOT NULL |
| matricula     | VARCHAR(15)  | FK -> VEHICULO(matricula), NOT NULL  |
| fecha\_inicio | DATE         | NOT NULL                             |
| fecha\_fin    | DATE         | NOT NULL                             |

### SERVICIO

| Atributo         | Tipo de dato | Restricciones |
| ------------------ | -------------- | --------------- |
| id\_servicio     | INT          | PK, NOT NULL  |
| nombre\_servicio | VARCHAR(150) | NOT NULL      |

### ALQUILER\_SERVICIO

| Atributo          | Tipo de dato  | Restricciones                              |
| ------------------- | --------------- | -------------------------------------------- |
| id\_alquiler      | INT           | PK, FK -> ALQUILER(id\_alquiler), NOT NULL |
| id\_servicio      | INT           | PK, FK -> SERVICIO(id\_servicio), NOT NULL |
| unidades          | INT           | NOT NULL                                   |
| importe\_aplicado | DECIMAL(10,2) | NOT NULL                                   |

## Primera Forma Normal (1FN)

### CLIENTE

| Atributo    | Tipo de dato | Restricciones    |
| ------------- | -------------- | ------------------ |
| id\_cliente | INT          | PK, NOT NULL     |
| nombre      | VARCHAR(100) | NOT NULL         |
| correo      | VARCHAR(150) | UNIQUE, NOT NULL |

### CLIENTE\_TELEFONO

| Atributo    | Tipo de dato | Restricciones                            |
| ------------- | -------------- | ------------------------------------------ |
| id\_cliente | INT          | PK, FK -> CLIENTE(id\_cliente), NOT NULL |
| telefono    | VARCHAR(20)  | PK, NOT NULL                             |

## Segunda Forma Normal (2FN)

### ALQUILER\_SERVICIO

| Atributo          | Tipo de dato  | Restricciones                              |
| ------------------- | --------------- | -------------------------------------------- |
| id\_alquiler      | INT           | PK, FK -> ALQUILER(id\_alquiler), NOT NULL |
| id\_servicio      | INT           | PK, FK -> SERVICIO(id\_servicio), NOT NULL |
| unidades          | INT           | NOT NULL                                   |
| importe\_aplicado | DECIMAL(10,2) | NOT NULL                                   |

## Tercera Forma Normal (3FN)

### VEHICULO

| Atributo    | Tipo de dato | Restricciones                            |
| ------------- | -------------- | ------------------------------------------ |
| matricula   | VARCHAR(15)  | PK, NOT NULL                             |
| modelo      | VARCHAR(100) | NOT NULL                                 |
| id\_tipo    | INT          | FK -> TIPO\_VEHICULO(id\_tipo), NOT NULL |
| id\_oficina | INT          | FK -> OFICINA(id\_oficina), NOT NULL     |

### TIPO\_VEHICULO

| Atributo          | Tipo de dato  | Restricciones |
| ------------------- | --------------- | --------------- |
| id\_tipo          | INT           | PK, NOT NULL  |
| descripcion\_tipo | VARCHAR(100)  | NOT NULL      |
| tarifa\_base      | DECIMAL(10,2) | NOT NULL      |

## Diagrama relacional final

```mermaid
erDiagram
    CLIENTE {
        INT id_cliente PK
        VARCHAR nombre
        VARCHAR correo UK
    }

    CLIENTE_TELEFONO {
        INT id_cliente PK, FK
        VARCHAR telefono PK
    }

    OFICINA {
        INT id_oficina PK
    }

    TIPO_VEHICULO {
        INT id_tipo PK
        VARCHAR descripcion_tipo
        DECIMAL tarifa_base
    }

    VEHICULO {
        VARCHAR matricula PK
        VARCHAR modelo
        INT id_tipo FK
        INT id_oficina FK
    }

    ALQUILER {
        INT id_alquiler PK
        INT id_cliente FK
        VARCHAR matricula FK
        DATE fecha_inicio
        DATE fecha_fin
    }

    SERVICIO {
        INT id_servicio PK
        VARCHAR nombre_servicio
    }

    ALQUILER_SERVICIO {
        INT id_alquiler PK, FK
        INT id_servicio PK, FK
        INT unidades
        DECIMAL importe_aplicado
    }

    CLIENTE ||--o{ CLIENTE_TELEFONO : tiene
    OFICINA ||--o{ VEHICULO : aloja
    TIPO_VEHICULO ||--o{ VEHICULO : clasifica
    CLIENTE ||--o{ ALQUILER : realiza
    VEHICULO ||--o{ ALQUILER : se_alquila
    ALQUILER ||--o{ ALQUILER_SERVICIO : incluye
    SERVICIO ||--o{ ALQUILER_SERVICIO : se_contrata
```

# V6 - ORGANIZACIÓN DE EVENTOS

## Modelo relacional inicial

### ASISTENTE

| Atributo      | Tipo de dato | Restricciones    |
| --------------- | -------------- | ------------------ |
| id\_asistente | INT          | PK, NOT NULL     |
| nombre        | VARCHAR(100) | NOT NULL         |
| correo        | VARCHAR(150) | UNIQUE, NOT NULL |

### ASISTENTE\_TELEFONO

| Atributo      | Tipo de dato | Restricciones                                |
| --------------- | -------------- | ---------------------------------------------- |
| id\_asistente | INT          | PK, FK -> ASISTENTE(id\_asistente), NOT NULL |
| telefono      | VARCHAR(20)  | PK, NOT NULL                                 |

### SALA

| Atributo  | Tipo de dato | Restricciones |
| ----------- | -------------- | --------------- |
| id\_sala  | INT          | PK, NOT NULL  |
| ubicacion | VARCHAR(150) | NOT NULL      |
| capacidad | INT          | NOT NULL      |

### EVENTO

| Atributo       | Tipo de dato | Restricciones                  |
| ---------------- | -------------- | -------------------------------- |
| id\_evento     | INT          | PK, NOT NULL                   |
| nombre\_evento | VARCHAR(150) | NOT NULL                       |
| id\_sala       | INT          | FK -> SALA(id\_sala), NOT NULL |
| fecha\_evento  | DATETIME     | NOT NULL                       |

### EMPLEADO

| Atributo     | Tipo de dato | Restricciones    |
| -------------- | -------------- | ------------------ |
| id\_empleado | INT          | PK, NOT NULL     |
| nombre       | VARCHAR(100) | NOT NULL         |
| correo       | VARCHAR(150) | UNIQUE, NOT NULL |

### TIPO\_ENTRADA

| Atributo           | Tipo de dato  | Restricciones |
| -------------------- | --------------- | --------------- |
| id\_tipo\_entrada  | INT           | PK, NOT NULL  |
| descripcion\_tipo  | VARCHAR(100)  | NOT NULL      |
| precio\_referencia | DECIMAL(10,2) | NOT NULL      |

> La clave compuesta supone una sola inscripción por asistente y evento. Si se admiten varias inscripciones para el mismo evento, debe revisarse la clave.

### INSCRIPCION

| Atributo          | Tipo de dato | Restricciones                                    |
| ------------------- | -------------- | -------------------------------------------------- |
| id\_asistente     | INT          | PK, FK -> ASISTENTE(id\_asistente), NOT NULL     |
| id\_evento        | INT          | PK, FK -> EVENTO(id\_evento), NOT NULL           |
| id\_tipo\_entrada | INT          | FK -> TIPO\_ENTRADA(id\_tipo\_entrada), NOT NULL |
| fecha             | DATETIME     | NOT NULL                                         |
| estado            | VARCHAR(30)  | NOT NULL                                         |

### COLABORACION

| Atributo     | Tipo de dato | Restricciones                              |
| -------------- | -------------- | -------------------------------------------- |
| id\_empleado | INT          | PK, FK -> EMPLEADO(id\_empleado), NOT NULL |
| id\_evento   | INT          | PK, FK -> EVENTO(id\_evento), NOT NULL     |
| funcion      | VARCHAR(100) | NOT NULL                                   |

## Primera Forma Normal (1FN)

### ASISTENTE

| Atributo      | Tipo de dato | Restricciones    |
| --------------- | -------------- | ------------------ |
| id\_asistente | INT          | PK, NOT NULL     |
| nombre        | VARCHAR(100) | NOT NULL         |
| correo        | VARCHAR(150) | UNIQUE, NOT NULL |

### ASISTENTE\_TELEFONO

| Atributo      | Tipo de dato | Restricciones                                |
| --------------- | -------------- | ---------------------------------------------- |
| id\_asistente | INT          | PK, FK -> ASISTENTE(id\_asistente), NOT NULL |
| telefono      | VARCHAR(20)  | PK, NOT NULL                                 |

## Segunda Forma Normal (2FN)

### INSCRIPCION

| Atributo          | Tipo de dato | Restricciones                                    |
| ------------------- | -------------- | -------------------------------------------------- |
| id\_asistente     | INT          | PK, FK -> ASISTENTE(id\_asistente), NOT NULL     |
| id\_evento        | INT          | PK, FK -> EVENTO(id\_evento), NOT NULL           |
| id\_tipo\_entrada | INT          | FK -> TIPO\_ENTRADA(id\_tipo\_entrada), NOT NULL |
| fecha             | DATETIME     | NOT NULL                                         |
| estado            | VARCHAR(30)  | NOT NULL                                         |

### COLABORACION

| Atributo     | Tipo de dato | Restricciones                              |
| -------------- | -------------- | -------------------------------------------- |
| id\_empleado | INT          | PK, FK -> EMPLEADO(id\_empleado), NOT NULL |
| id\_evento   | INT          | PK, FK -> EVENTO(id\_evento), NOT NULL     |
| funcion      | VARCHAR(100) | NOT NULL                                   |

## Tercera Forma Normal (3FN)

### EVENTO

| Atributo       | Tipo de dato | Restricciones                  |
| ---------------- | -------------- | -------------------------------- |
| id\_evento     | INT          | PK, NOT NULL                   |
| nombre\_evento | VARCHAR(150) | NOT NULL                       |
| id\_sala       | INT          | FK -> SALA(id\_sala), NOT NULL |
| fecha\_evento  | DATETIME     | NOT NULL                       |

### SALA

| Atributo  | Tipo de dato | Restricciones |
| ----------- | -------------- | --------------- |
| id\_sala  | INT          | PK, NOT NULL  |
| ubicacion | VARCHAR(150) | NOT NULL      |
| capacidad | INT          | NOT NULL      |

## Diagrama relacional final

```mermaid
erDiagram
    ASISTENTE {
        INT id_asistente PK
        VARCHAR nombre
        VARCHAR correo UK
    }

    ASISTENTE_TELEFONO {
        INT id_asistente PK, FK
        VARCHAR telefono PK
    }

    SALA {
        INT id_sala PK
        VARCHAR ubicacion
        INT capacidad
    }

    EVENTO {
        INT id_evento PK
        VARCHAR nombre_evento
        INT id_sala FK
        DATETIME fecha_evento
    }

    EMPLEADO {
        INT id_empleado PK
        VARCHAR nombre
        VARCHAR correo UK
    }

    TIPO_ENTRADA {
        INT id_tipo_entrada PK
        VARCHAR descripcion_tipo
        DECIMAL precio_referencia
    }

    INSCRIPCION {
        INT id_asistente PK, FK
        INT id_evento PK, FK
        INT id_tipo_entrada FK
        DATETIME fecha
        VARCHAR estado
    }

    COLABORACION {
        INT id_empleado PK, FK
        INT id_evento PK, FK
        VARCHAR funcion
    }

    ASISTENTE ||--o{ ASISTENTE_TELEFONO : tiene
    SALA ||--o{ EVENTO : alberga
    ASISTENTE ||--o{ INSCRIPCION : realiza
    EVENTO ||--o{ INSCRIPCION : recibe
    TIPO_ENTRADA ||--o{ INSCRIPCION : clasifica
    EMPLEADO ||--o{ COLABORACION : participa
    EVENTO ||--o{ COLABORACION : recibe
```

# V7 - AGENCIA DE VIAJES

## Modelo relacional inicial

### CLIENTE

| Atributo    | Tipo de dato | Restricciones    |
| ------------- | -------------- | ------------------ |
| id\_cliente | INT          | PK, NOT NULL     |
| nombre      | VARCHAR(100) | NOT NULL         |
| correo      | VARCHAR(150) | UNIQUE, NOT NULL |

### CLIENTE\_TELEFONO

| Atributo    | Tipo de dato | Restricciones                            |
| ------------- | -------------- | ------------------------------------------ |
| id\_cliente | INT          | PK, FK -> CLIENTE(id\_cliente), NOT NULL |
| telefono    | VARCHAR(20)  | PK, NOT NULL                             |

### DESTINO

| Atributo        | Tipo de dato | Restricciones |
| ----------------- | -------------- | --------------- |
| id\_destino     | INT          | PK, NOT NULL  |
| nombre\_destino | VARCHAR(150) | NOT NULL      |
| pais            | VARCHAR(100) | NOT NULL      |

### HOTEL

| Atributo      | Tipo de dato | Restricciones                        |
| --------------- | -------------- | -------------------------------------- |
| id\_hotel     | INT          | PK, NOT NULL                         |
| nombre\_hotel | VARCHAR(150) | NOT NULL                             |
| id\_destino   | INT          | FK -> DESTINO(id\_destino), NOT NULL |

### RESERVA

| Atributo       | Tipo de dato | Restricciones                        |
| ---------------- | -------------- | -------------------------------------- |
| id\_reserva    | INT          | PK, NOT NULL                         |
| id\_cliente    | INT          | FK -> CLIENTE(id\_cliente), NOT NULL |
| id\_hotel      | INT          | FK -> HOTEL(id\_hotel), NOT NULL     |
| fecha\_entrada | DATE         | NOT NULL                             |
| fecha\_salida  | DATE         | NOT NULL                             |

### EXCURSION

| Atributo          | Tipo de dato  | Restricciones |
| ------------------- | --------------- | --------------- |
| id\_excursion     | INT           | PK, NOT NULL  |
| nombre\_excursion | VARCHAR(150)  | NOT NULL      |
| precio            | DECIMAL(10,2) | NOT NULL      |

### RESERVA\_EXCURSION

| Atributo              | Tipo de dato | Restricciones                                |
| ----------------------- | -------------- | ---------------------------------------------- |
| id\_reserva           | INT          | PK, FK -> RESERVA(id\_reserva), NOT NULL     |
| id\_excursion         | INT          | PK, FK -> EXCURSION(id\_excursion), NOT NULL |
| numero\_participantes | INT          | NOT NULL                                     |

## Primera Forma Normal (1FN)

### CLIENTE

| Atributo    | Tipo de dato | Restricciones    |
| ------------- | -------------- | ------------------ |
| id\_cliente | INT          | PK, NOT NULL     |
| nombre      | VARCHAR(100) | NOT NULL         |
| correo      | VARCHAR(150) | UNIQUE, NOT NULL |

### CLIENTE\_TELEFONO

| Atributo    | Tipo de dato | Restricciones                            |
| ------------- | -------------- | ------------------------------------------ |
| id\_cliente | INT          | PK, FK -> CLIENTE(id\_cliente), NOT NULL |
| telefono    | VARCHAR(20)  | PK, NOT NULL                             |

## Segunda Forma Normal (2FN)

### RESERVA\_EXCURSION

| Atributo              | Tipo de dato | Restricciones                                |
| ----------------------- | -------------- | ---------------------------------------------- |
| id\_reserva           | INT          | PK, FK -> RESERVA(id\_reserva), NOT NULL     |
| id\_excursion         | INT          | PK, FK -> EXCURSION(id\_excursion), NOT NULL |
| numero\_participantes | INT          | NOT NULL                                     |

## Tercera Forma Normal (3FN)

### HOTEL

| Atributo      | Tipo de dato | Restricciones                        |
| --------------- | -------------- | -------------------------------------- |
| id\_hotel     | INT          | PK, NOT NULL                         |
| nombre\_hotel | VARCHAR(150) | NOT NULL                             |
| id\_destino   | INT          | FK -> DESTINO(id\_destino), NOT NULL |

### DESTINO

| Atributo        | Tipo de dato | Restricciones |
| ----------------- | -------------- | --------------- |
| id\_destino     | INT          | PK, NOT NULL  |
| nombre\_destino | VARCHAR(150) | NOT NULL      |
| pais            | VARCHAR(100) | NOT NULL      |

## Diagrama relacional final

```mermaid
erDiagram
    CLIENTE {
        INT id_cliente PK
        VARCHAR nombre
        VARCHAR correo UK
    }

    CLIENTE_TELEFONO {
        INT id_cliente PK, FK
        VARCHAR telefono PK
    }

    DESTINO {
        INT id_destino PK
        VARCHAR nombre_destino
        VARCHAR pais
    }

    HOTEL {
        INT id_hotel PK
        VARCHAR nombre_hotel
        INT id_destino FK
    }

    RESERVA {
        INT id_reserva PK
        INT id_cliente FK
        INT id_hotel FK
        DATE fecha_entrada
        DATE fecha_salida
    }

    EXCURSION {
        INT id_excursion PK
        VARCHAR nombre_excursion
        DECIMAL precio
    }

    RESERVA_EXCURSION {
        INT id_reserva PK, FK
        INT id_excursion PK, FK
        INT numero_participantes
    }

    CLIENTE ||--o{ CLIENTE_TELEFONO : tiene
    CLIENTE ||--o{ RESERVA : realiza
    DESTINO ||--o{ HOTEL : contiene
    HOTEL ||--o{ RESERVA : recibe
    RESERVA ||--o{ RESERVA_EXCURSION : incluye
    EXCURSION ||--o{ RESERVA_EXCURSION : se_reserva
```

# V8 - EMPRESA DE DESARROLLO DE SOFTWARE

## Modelo relacional inicial

### EMPLEADO

| Atributo     | Tipo de dato | Restricciones    |
| -------------- | -------------- | ------------------ |
| id\_empleado | INT          | PK, NOT NULL     |
| nombre       | VARCHAR(100) | NOT NULL         |
| correo       | VARCHAR(150) | UNIQUE, NOT NULL |

### EMPLEADO\_TELEFONO

| Atributo     | Tipo de dato | Restricciones                              |
| -------------- | -------------- | -------------------------------------------- |
| id\_empleado | INT          | PK, FK -> EMPLEADO(id\_empleado), NOT NULL |
| telefono     | VARCHAR(20)  | PK, NOT NULL                               |

### DEPARTAMENTO

| Atributo             | Tipo de dato | Restricciones |
| ---------------------- | -------------- | --------------- |
| id\_departamento     | INT          | PK, NOT NULL  |
| nombre\_departamento | VARCHAR(150) | NOT NULL      |

### PROYECTO

| Atributo         | Tipo de dato | Restricciones                                  |
| ------------------ | -------------- | ------------------------------------------------ |
| id\_proyecto     | INT          | PK, NOT NULL                                   |
| nombre\_proyecto | VARCHAR(150) | NOT NULL                                       |
| id\_departamento | INT          | FK -> DEPARTAMENTO(id\_departamento), NOT NULL |

### TAREA

| Atributo     | Tipo de dato | Restricciones                          |
| -------------- | -------------- | ---------------------------------------- |
| id\_tarea    | INT          | PK, NOT NULL                           |
| id\_proyecto | INT          | FK -> PROYECTO(id\_proyecto), NOT NULL |
| descripcion  | VARCHAR(250) | NOT NULL                               |
| prioridad    | VARCHAR(30)  | NOT NULL                               |

### TECNOLOGIA

| Atributo           | Tipo de dato | Restricciones |
| -------------------- | -------------- | --------------- |
| id\_tecnologia     | INT          | PK, NOT NULL  |
| nombre\_tecnologia | VARCHAR(100) | NOT NULL      |

> La clave compuesta supone una única asignación vigente por empleado y proyecto. Si se necesita guardar varias asignaciones históricas para la misma pareja, debe incorporarse un identificador o un atributo temporal a la clave.

### EMPLEADO\_PROYECTO

| Atributo               | Tipo de dato | Restricciones                              |
| ------------------------ | -------------- | -------------------------------------------- |
| id\_empleado           | INT          | PK, FK -> EMPLEADO(id\_empleado), NOT NULL |
| id\_proyecto           | INT          | PK, FK -> PROYECTO(id\_proyecto), NOT NULL |
| fecha\_incorporacion   | DATE         | NOT NULL                                   |
| porcentaje\_dedicacion | DECIMAL(5,2) | NOT NULL                                   |

### PROYECTO\_TECNOLOGIA

| Atributo       | Tipo de dato | Restricciones                                  |
| ---------------- | -------------- | ------------------------------------------------ |
| id\_proyecto   | INT          | PK, FK -> PROYECTO(id\_proyecto), NOT NULL     |
| id\_tecnologia | INT          | PK, FK -> TECNOLOGIA(id\_tecnologia), NOT NULL |

## Primera Forma Normal (1FN)

### EMPLEADO

| Atributo     | Tipo de dato | Restricciones    |
| -------------- | -------------- | ------------------ |
| id\_empleado | INT          | PK, NOT NULL     |
| nombre       | VARCHAR(100) | NOT NULL         |
| correo       | VARCHAR(150) | UNIQUE, NOT NULL |

### EMPLEADO\_TELEFONO

| Atributo     | Tipo de dato | Restricciones                              |
| -------------- | -------------- | -------------------------------------------- |
| id\_empleado | INT          | PK, FK -> EMPLEADO(id\_empleado), NOT NULL |
| telefono     | VARCHAR(20)  | PK, NOT NULL                               |

## Segunda Forma Normal (2FN)

### EMPLEADO\_PROYECTO

| Atributo               | Tipo de dato | Restricciones                              |
| ------------------------ | -------------- | -------------------------------------------- |
| id\_empleado           | INT          | PK, FK -> EMPLEADO(id\_empleado), NOT NULL |
| id\_proyecto           | INT          | PK, FK -> PROYECTO(id\_proyecto), NOT NULL |
| fecha\_incorporacion   | DATE         | NOT NULL                                   |
| porcentaje\_dedicacion | DECIMAL(5,2) | NOT NULL                                   |

### PROYECTO\_TECNOLOGIA

| Atributo       | Tipo de dato | Restricciones                                  |
| ---------------- | -------------- | ------------------------------------------------ |
| id\_proyecto   | INT          | PK, FK -> PROYECTO(id\_proyecto), NOT NULL     |
| id\_tecnologia | INT          | PK, FK -> TECNOLOGIA(id\_tecnologia), NOT NULL |

## Tercera Forma Normal (3FN)

### PROYECTO

| Atributo         | Tipo de dato | Restricciones                                  |
| ------------------ | -------------- | ------------------------------------------------ |
| id\_proyecto     | INT          | PK, NOT NULL                                   |
| nombre\_proyecto | VARCHAR(150) | NOT NULL                                       |
| id\_departamento | INT          | FK -> DEPARTAMENTO(id\_departamento), NOT NULL |

### DEPARTAMENTO

| Atributo             | Tipo de dato | Restricciones |
| ---------------------- | -------------- | --------------- |
| id\_departamento     | INT          | PK, NOT NULL  |
| nombre\_departamento | VARCHAR(150) | NOT NULL      |

## Diagrama relacional final

```mermaid
erDiagram
    EMPLEADO {
        INT id_empleado PK
        VARCHAR nombre
        VARCHAR correo UK
    }

    EMPLEADO_TELEFONO {
        INT id_empleado PK, FK
        VARCHAR telefono PK
    }

    DEPARTAMENTO {
        INT id_departamento PK
        VARCHAR nombre_departamento
    }

    PROYECTO {
        INT id_proyecto PK
        VARCHAR nombre_proyecto
        INT id_departamento FK
    }

    TAREA {
        INT id_tarea PK
        INT id_proyecto FK
        VARCHAR descripcion
        VARCHAR prioridad
    }

    TECNOLOGIA {
        INT id_tecnologia PK
        VARCHAR nombre_tecnologia
    }

    EMPLEADO_PROYECTO {
        INT id_empleado PK, FK
        INT id_proyecto PK, FK
        DATE fecha_incorporacion
        DECIMAL porcentaje_dedicacion
    }

    PROYECTO_TECNOLOGIA {
        INT id_proyecto PK, FK
        INT id_tecnologia PK, FK
    }

    EMPLEADO ||--o{ EMPLEADO_TELEFONO : tiene
    DEPARTAMENTO ||--o{ PROYECTO : organiza
    PROYECTO ||--o{ TAREA : contiene
    EMPLEADO ||--o{ EMPLEADO_PROYECTO : participa
    PROYECTO ||--o{ EMPLEADO_PROYECTO : asigna
    PROYECTO ||--o{ PROYECTO_TECNOLOGIA : utiliza
    TECNOLOGIA ||--o{ PROYECTO_TECNOLOGIA : aparece
```

# V9 - MUSEO

## Modelo relacional inicial

### VISITANTE

| Atributo      | Tipo de dato | Restricciones    |
| --------------- | -------------- | ------------------ |
| id\_visitante | INT          | PK, NOT NULL     |
| nombre        | VARCHAR(100) | NOT NULL         |
| correo        | VARCHAR(150) | UNIQUE, NOT NULL |

### VISITANTE\_TELEFONO

| Atributo      | Tipo de dato | Restricciones                                |
| --------------- | -------------- | ---------------------------------------------- |
| id\_visitante | INT          | PK, FK -> VISITANTE(id\_visitante), NOT NULL |
| telefono      | VARCHAR(20)  | PK, NOT NULL                                 |

### SALA

| Atributo        | Tipo de dato | Restricciones |
| ----------------- | -------------- | --------------- |
| id\_sala        | INT          | PK, NOT NULL  |
| ubicacion\_sala | VARCHAR(150) | NOT NULL      |

### EXPOSICION

| Atributo           | Tipo de dato | Restricciones                  |
| -------------------- | -------------- | -------------------------------- |
| id\_exposicion     | INT          | PK, NOT NULL                   |
| nombre\_exposicion | VARCHAR(150) | NOT NULL                       |
| id\_sala           | INT          | FK -> SALA(id\_sala), NOT NULL |
| fecha\_inicio      | DATE         | NOT NULL                       |

### OBRA

| Atributo       | Tipo de dato | Restricciones |
| ---------------- | -------------- | --------------- |
| id\_obra       | INT          | PK, NOT NULL  |
| titulo         | VARCHAR(200) | NOT NULL      |
| anio\_creacion | INT          | NULL          |

### ARTISTA

| Atributo        | Tipo de dato | Restricciones |
| ----------------- | -------------- | --------------- |
| id\_artista     | INT          | PK, NOT NULL  |
| nombre\_artista | VARCHAR(150) | NOT NULL      |

### OBRA\_ARTISTA

| Atributo    | Tipo de dato | Restricciones                            |
| ------------- | -------------- | ------------------------------------------ |
| id\_obra    | INT          | PK, FK -> OBRA(id\_obra), NOT NULL       |
| id\_artista | INT          | PK, FK -> ARTISTA(id\_artista), NOT NULL |

### EXPOSICION\_OBRA

| Atributo             | Tipo de dato | Restricciones                                  |
| ---------------------- | -------------- | ------------------------------------------------ |
| id\_exposicion       | INT          | PK, FK -> EXPOSICION(id\_exposicion), NOT NULL |
| id\_obra             | INT          | PK, FK -> OBRA(id\_obra), NOT NULL             |
| fecha\_incorporacion | DATE         | NOT NULL                                       |
| posicion             | INT          | NOT NULL                                       |

## Primera Forma Normal (1FN)

### VISITANTE

| Atributo      | Tipo de dato | Restricciones    |
| --------------- | -------------- | ------------------ |
| id\_visitante | INT          | PK, NOT NULL     |
| nombre        | VARCHAR(100) | NOT NULL         |
| correo        | VARCHAR(150) | UNIQUE, NOT NULL |

### VISITANTE\_TELEFONO

| Atributo      | Tipo de dato | Restricciones                                |
| --------------- | -------------- | ---------------------------------------------- |
| id\_visitante | INT          | PK, FK -> VISITANTE(id\_visitante), NOT NULL |
| telefono      | VARCHAR(20)  | PK, NOT NULL                                 |

## Segunda Forma Normal (2FN)

### OBRA\_ARTISTA

| Atributo    | Tipo de dato | Restricciones                            |
| ------------- | -------------- | ------------------------------------------ |
| id\_obra    | INT          | PK, FK -> OBRA(id\_obra), NOT NULL       |
| id\_artista | INT          | PK, FK -> ARTISTA(id\_artista), NOT NULL |

### EXPOSICION\_OBRA

| Atributo             | Tipo de dato | Restricciones                                  |
| ---------------------- | -------------- | ------------------------------------------------ |
| id\_exposicion       | INT          | PK, FK -> EXPOSICION(id\_exposicion), NOT NULL |
| id\_obra             | INT          | PK, FK -> OBRA(id\_obra), NOT NULL             |
| fecha\_incorporacion | DATE         | NOT NULL                                       |
| posicion             | INT          | NOT NULL                                       |

## Tercera Forma Normal (3FN)

### EXPOSICION

| Atributo           | Tipo de dato | Restricciones                  |
| -------------------- | -------------- | -------------------------------- |
| id\_exposicion     | INT          | PK, NOT NULL                   |
| nombre\_exposicion | VARCHAR(150) | NOT NULL                       |
| id\_sala           | INT          | FK -> SALA(id\_sala), NOT NULL |
| fecha\_inicio      | DATE         | NOT NULL                       |

### SALA

| Atributo        | Tipo de dato | Restricciones |
| ----------------- | -------------- | --------------- |
| id\_sala        | INT          | PK, NOT NULL  |
| ubicacion\_sala | VARCHAR(150) | NOT NULL      |

## Diagrama relacional final

```mermaid
erDiagram
    VISITANTE {
        INT id_visitante PK
        VARCHAR nombre
        VARCHAR correo UK
    }

    VISITANTE_TELEFONO {
        INT id_visitante PK, FK
        VARCHAR telefono PK
    }

    SALA {
        INT id_sala PK
        VARCHAR ubicacion_sala
    }

    EXPOSICION {
        INT id_exposicion PK
        VARCHAR nombre_exposicion
        INT id_sala FK
        DATE fecha_inicio
    }

    OBRA {
        INT id_obra PK
        VARCHAR titulo
        INT anio_creacion
    }

    ARTISTA {
        INT id_artista PK
        VARCHAR nombre_artista
    }

    OBRA_ARTISTA {
        INT id_obra PK, FK
        INT id_artista PK, FK
    }

    EXPOSICION_OBRA {
        INT id_exposicion PK, FK
        INT id_obra PK, FK
        DATE fecha_incorporacion
        INT posicion
    }

    VISITANTE ||--o{ VISITANTE_TELEFONO : tiene
    SALA ||--o{ EXPOSICION : alberga
    OBRA ||--o{ OBRA_ARTISTA : relaciona
    ARTISTA ||--o{ OBRA_ARTISTA : crea
    EXPOSICION ||--o{ EXPOSICION_OBRA : incluye
    OBRA ||--o{ EXPOSICION_OBRA : aparece
```

# V10 - TRANSPORTE DE PASAJEROS

## Modelo relacional inicial

### PASAJERO

| Atributo     | Tipo de dato | Restricciones    |
| -------------- | -------------- | ------------------ |
| id\_pasajero | INT          | PK, NOT NULL     |
| nombre       | VARCHAR(100) | NOT NULL         |
| documento    | VARCHAR(30)  | UNIQUE, NOT NULL |

### PASAJERO\_TELEFONO

| Atributo     | Tipo de dato | Restricciones                              |
| -------------- | -------------- | -------------------------------------------- |
| id\_pasajero | INT          | PK, FK -> PASAJERO(id\_pasajero), NOT NULL |
| telefono     | VARCHAR(20)  | PK, NOT NULL                               |

### RUTA

| Atributo | Tipo de dato | Restricciones |
| ---------- | -------------- | --------------- |
| id\_ruta | INT          | PK, NOT NULL  |
| origen   | VARCHAR(150) | NOT NULL      |
| destino  | VARCHAR(150) | NOT NULL      |

### VEHICULO

| Atributo     | Tipo de dato | Restricciones    |
| -------------- | -------------- | ------------------ |
| id\_vehiculo | INT          | PK, NOT NULL     |
| matricula    | VARCHAR(15)  | UNIQUE, NOT NULL |
| capacidad    | INT          | NOT NULL         |

### SERVICIO

| Atributo            | Tipo de dato | Restricciones                          |
| --------------------- | -------------- | ---------------------------------------- |
| id\_servicio        | INT          | PK, NOT NULL                           |
| id\_ruta            | INT          | FK -> RUTA(id\_ruta), NOT NULL         |
| id\_vehiculo        | INT          | FK -> VEHICULO(id\_vehiculo), NOT NULL |
| fecha\_hora\_salida | DATETIME     | NOT NULL                               |

### BILLETE

| Atributo       | Tipo de dato  | Restricciones                          |
| ---------------- | --------------- | ---------------------------------------- |
| id\_billete    | INT           | PK, NOT NULL                           |
| id\_pasajero   | INT           | FK -> PASAJERO(id\_pasajero), NOT NULL |
| id\_servicio   | INT           | FK -> SERVICIO(id\_servicio), NOT NULL |
| fecha\_compra  | DATETIME      | NOT NULL                               |
| asiento        | VARCHAR(10)   | NOT NULL                               |
| precio\_pagado | DECIMAL(10,2) | NOT NULL                               |

## Primera Forma Normal (1FN)

### PASAJERO

| Atributo     | Tipo de dato | Restricciones    |
| -------------- | -------------- | ------------------ |
| id\_pasajero | INT          | PK, NOT NULL     |
| nombre       | VARCHAR(100) | NOT NULL         |
| documento    | VARCHAR(30)  | UNIQUE, NOT NULL |

### PASAJERO\_TELEFONO

| Atributo     | Tipo de dato | Restricciones                              |
| -------------- | -------------- | -------------------------------------------- |
| id\_pasajero | INT          | PK, FK -> PASAJERO(id\_pasajero), NOT NULL |
| telefono     | VARCHAR(20)  | PK, NOT NULL                               |

## Segunda Forma Normal (2FN)

> **Nota:** `BILLETE` tiene una clave primaria simple (`id_billete`), por lo que no puede presentar dependencias parciales de una clave compuesta. En consecuencia, ya cumple 2FN si cumple 1FN; esta sección documenta su estado y no una descomposición adicional.

### BILLETE

| Atributo       | Tipo de dato  | Restricciones                          |
| ---------------- | --------------- | ---------------------------------------- |
| id\_billete    | INT           | PK, NOT NULL                           |
| id\_pasajero   | INT           | FK -> PASAJERO(id\_pasajero), NOT NULL |
| id\_servicio   | INT           | FK -> SERVICIO(id\_servicio), NOT NULL |
| fecha\_compra  | DATETIME      | NOT NULL                               |
| asiento        | VARCHAR(10)   | NOT NULL                               |
| precio\_pagado | DECIMAL(10,2) | NOT NULL                               |

## Tercera Forma Normal (3FN)

### SERVICIO

| Atributo            | Tipo de dato | Restricciones                          |
| --------------------- | -------------- | ---------------------------------------- |
| id\_servicio        | INT          | PK, NOT NULL                           |
| id\_ruta            | INT          | FK -> RUTA(id\_ruta), NOT NULL         |
| id\_vehiculo        | INT          | FK -> VEHICULO(id\_vehiculo), NOT NULL |
| fecha\_hora\_salida | DATETIME     | NOT NULL                               |

### RUTA

| Atributo | Tipo de dato | Restricciones |
| ---------- | -------------- | --------------- |
| id\_ruta | INT          | PK, NOT NULL  |
| origen   | VARCHAR(150) | NOT NULL      |
| destino  | VARCHAR(150) | NOT NULL      |

## Diagrama relacional final

```mermaid
erDiagram
    PASAJERO {
        INT id_pasajero PK
        VARCHAR nombre
        VARCHAR documento UK
    }

    PASAJERO_TELEFONO {
        INT id_pasajero PK, FK
        VARCHAR telefono PK
    }

    RUTA {
        INT id_ruta PK
        VARCHAR origen
        VARCHAR destino
    }

    VEHICULO {
        INT id_vehiculo PK
        VARCHAR matricula UK
        INT capacidad
    }

    SERVICIO {
        INT id_servicio PK
        INT id_ruta FK
        INT id_vehiculo FK
        DATETIME fecha_hora_salida
    }

    BILLETE {
        INT id_billete PK
        INT id_pasajero FK
        INT id_servicio FK
        DATETIME fecha_compra
        VARCHAR asiento
        DECIMAL precio_pagado
    }

    PASAJERO ||--o{ PASAJERO_TELEFONO : tiene
    PASAJERO ||--o{ BILLETE : compra
    SERVICIO ||--o{ BILLETE : incluye
    RUTA ||--o{ SERVICIO : define
    VEHICULO ||--o{ SERVICIO : asigna
```



