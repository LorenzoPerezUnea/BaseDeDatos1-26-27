# Variante v1 — Clínica

## Entidades

PACIENTE, CITA, MÉDICO, TRATAMIENTO

## Matriz de relaciones

| Relación                 | Entidad 1 | Cardinalidad | Participación | Entidad 2   | Cardinalidad | Participación |
| --------------------------- | ----------- | -------------- | ---------------- | ------------- | -------------- | ---------------- |
| TIENE / CORRESPONDE A     | PACIENTE  | (0,N)        | Opcional       | CITA        | (1,1)        | Obligatoria    |
| ATIENDE / ES ATENDIDO POR | MÉDICO   | (0,N)        | Opcional       | CITA        | (1,1)        | Obligatoria    |
| RECIBE / SE APLICA EN     | CITA      | (0,N)        | Opcional       | TRATAMIENTO | (0,N)        | Opcional       |

## Mermaid

```mermaid
flowchart LR
    PACIENTE["PACIENTE"]
    CITA["CITA"]
    MEDICO["MÉDICO"]
    TRATAMIENTO["TRATAMIENTO"]

    TIENE{"TIENE / CORRESPONDE A"}
    ATIENDE{"ATIENDE / ES ATENDIDO POR"}
    APLICA{"RECIBE / SE APLICA EN"}

    ID_P(("identificador"))
    NOM_P(("nombre"))
    FECHA(("fecha"))
    MOTIVO(("motivo"))
    ID_T(("identificador"))
    DESC_T(("descripción"))

    PACIENTE --- ID_P
    PACIENTE --- NOM_P
    CITA --- FECHA
    CITA --- MOTIVO
    TRATAMIENTO --- ID_T
    TRATAMIENTO --- DESC_T

    PACIENTE ---|"0..N"| TIENE
    TIENE ---|"1..1"| CITA
    MEDICO ---|"0..N"| ATIENDE
    ATIENDE ---|"1..1"| CITA
    CITA ---|"0..N"| APLICA
    APLICA ---|"0..N"| TRATAMIENTO
```

# Variante v2 — Biblioteca

## Entidades

LIBRO, EDITORIAL, AUTOR, SOCIO, PRÉSTAMO

## Matriz de relaciones

| Relación                  | Entidad 1 | Cardinalidad | Participación | Entidad 2 | Cardinalidad | Participación |
| ---------------------------- | ----------- | -------------- | ---------------- | ----------- | -------------- | ---------------- |
| PUBLICA / ES PUBLICADO POR | EDITORIAL | (0,N)        | Opcional       | LIBRO     | (1,1)        | Obligatoria    |
| ESCRIBE / ES ESCRITO POR   | AUTOR     | (0,N)        | Opcional       | LIBRO     | (0,N)        | Opcional       |
| REALIZA / ES REALIZADO POR | SOCIO     | (0,N)        | Opcional       | PRÉSTAMO | (1,1)        | Obligatoria    |
| FIGURA EN / INCLUYE        | LIBRO     | (0,N)        | Opcional       | PRÉSTAMO | (1,1)        | Obligatoria    |

## Mermaid

```mermaid
flowchart LR
    LIBRO["LIBRO"]
    EDITORIAL["EDITORIAL"]
    AUTOR["AUTOR"]
    SOCIO["SOCIO"]
    PRESTAMO["PRÉSTAMO"]

    PUBLICA{"PUBLICA / ES PUBLICADO POR"}
    ESCRIBE{"ESCRIBE / ES ESCRITO POR"}
    REALIZA{"REALIZA / ES REALIZADO POR"}
    CORRESPONDE{"INCLUYE / FORMA PARTE DE"}

    ISBN(("ISBN"))
    TITULO(("título"))
    NOM_E(("nombre"))
    PAIS(("país"))
    ID_A(("identificador"))
    NOM_A(("nombre"))
    FECHA_I(("fecha de inicio"))
    FECHA_D(("fecha de devolución prevista"))

    LIBRO --- ISBN
    LIBRO --- TITULO
    EDITORIAL --- NOM_E
    EDITORIAL --- PAIS
    AUTOR --- ID_A
    AUTOR --- NOM_A
    PRESTAMO --- FECHA_I
    PRESTAMO --- FECHA_D

    EDITORIAL ---|"0..N"| PUBLICA
    PUBLICA ---|"1..1"| LIBRO
    AUTOR ---|"0..N"| ESCRIBE
    ESCRIBE ---|"0..N"| LIBRO
    SOCIO ---|"0..N"| REALIZA
    REALIZA ---|"1..1"| PRESTAMO
    LIBRO ---|"0..N"| CORRESPONDE
    CORRESPONDE ---|"1..1"| PRESTAMO
```

---

# Variante v3 — Agencia de viajes

## Entidades

DESTINO, HOTEL, CLIENTE, RESERVA, EXCURSIÓN

## Matriz de relaciones

| Relación                  | Entidad 1 | Cardinalidad | Participación | Entidad 2  | Cardinalidad | Participación |
| ---------------------------- | ----------- | -------------- | ---------------- | ------------ | -------------- | ---------------- |
| ALBERGA / ESTÁ SITUADO EN | DESTINO   | (0,N)        | Opcional       | HOTEL      | (1,1)        | Obligatoria    |
| REALIZA / ES REALIZADA POR | CLIENTE   | (0,N)        | Opcional       | RESERVA    | (1,1)        | Obligatoria    |
| SE INCLUYE EN / INCLUYE    | HOTEL     | (0,N)        | Opcional       | RESERVA    | (1,1)        | Obligatoria    |
| INCLUYE / FORMA PARTE DE   | RESERVA   | (0,N)        | Opcional       | EXCURSIÓN | (0,N)        | Opcional       |

## Mermaid

```mermaid
flowchart LR
    DESTINO["DESTINO"]
    HOTEL["HOTEL"]
    CLIENTE["CLIENTE"]
    RESERVA["RESERVA"]
    EXCURSION["EXCURSIÓN"]

    SITUADO{"ALBERGA / ESTÁ SITUADO EN"}
    REALIZA{"REALIZA / ES REALIZADA POR"}
    RESERVA_H{"SE INCLUYE EN / INCLUYE"}
    INCLUYE{"FIGURA EN / INCLUYE"}

    ID_D(("identificador"))
    NOM_D(("nombre"))
    ID_H(("identificador"))
    NOM_H(("nombre"))
    FECHA_E(("fecha de entrada"))
    FECHA_S(("fecha de salida"))
    ID_EX(("identificador"))
    DESC_EX(("descripción"))

    DESTINO --- ID_D
    DESTINO --- NOM_D
    HOTEL --- ID_H
    HOTEL --- NOM_H
    RESERVA --- FECHA_E
    RESERVA --- FECHA_S
    EXCURSION --- ID_EX
    EXCURSION --- DESC_EX

    DESTINO ---|"0..N"| SITUADO
    SITUADO ---|"1..1"| HOTEL
    CLIENTE ---|"0..N"| REALIZA
    REALIZA ---|"1..1"| RESERVA
    HOTEL ---|"0..N"| RESERVA_H
    RESERVA_H ---|"1..1"| RESERVA
    RESERVA ---|"0..N"| INCLUYE
    INCLUYE ---|"0..N"| EXCURSION
```

# Variante v4 — Universidad

## Entidades

TITULACIÓN, ASIGNATURA, PROFESOR, ESTUDIANTE, MATRÍCULA

## Matriz de relaciones

| Relación                                    | Entidad 1   | Cardinalidad | Participación | Entidad 2  | Cardinalidad | Participación |
| ---------------------------------------------- | ------------- | -------------- | ---------------- | ------------ | -------------- | ---------------- |
| INCLUYE / FORMA PARTE DE                     | TITULACIÓN | (0,N)        | Opcional       | ASIGNATURA | (1,1)        | Obligatoria    |
| IMPARTE / ES IMPARTIDA POR                   | PROFESOR    | (0,N)        | Opcional       | ASIGNATURA | (0,N)        | Opcional       |
| REALIZA / ES REALIZADA POR                   | ESTUDIANTE  | (0,N)        | Opcional       | MATRÍCULA | (1,1)        | Obligatoria    |
| TIENE MATRÍCULAS / CORRESPONDE A ASIGNATURA | ASIGNATURA  | (0,N)        | Opcional       | MATRÍCULA | (1,1)        | Obligatoria    |

## Mermaid

```mermaid
flowchart LR
    TITULACION["TITULACIÓN"]
    ASIGNATURA["ASIGNATURA"]
    PROFESOR["PROFESOR"]
    ESTUDIANTE["ESTUDIANTE"]
    MATRICULA["MATRÍCULA"]

    INCLUYE{"INCLUYE / FORMA PARTE DE"}
    IMPARTE{"IMPARTE / ES IMPARTIDA POR"}
    REALIZA{"REALIZA / ES REALIZADA POR"}
    CORRESPONDE{"TIENE MATRÍCULAS / CORRESPONDE A ASIGNATURA"}

    ID_T(("identificador"))
    NOM_T(("nombre"))
    ID_A(("identificador"))
    NOM_A(("nombre"))
    ID_P(("identificador"))
    CORREO(("correo"))
    FECHA(("fecha"))
    CALIFICACION(("calificación"))

    TITULACION --- ID_T
    TITULACION --- NOM_T
    ASIGNATURA --- ID_A
    ASIGNATURA --- NOM_A
    PROFESOR --- ID_P
    PROFESOR --- CORREO
    MATRICULA --- FECHA
    MATRICULA --- CALIFICACION

    TITULACION ---|"0..N"| INCLUYE
    INCLUYE ---|"1..1"| ASIGNATURA
    PROFESOR ---|"0..N"| IMPARTE
    IMPARTE ---|"0..N"| ASIGNATURA
    ESTUDIANTE ---|"0..N"| REALIZA
    REALIZA ---|"1..1"| MATRICULA
    ASIGNATURA ---|"0..N"| CORRESPONDE
    CORRESPONDE ---|"1..1"| MATRICULA
```

# Variante v5 — Empresa de alquiler

## Entidades

VEHÍCULO, OFICINA, CLIENTE, ALQUILER, SERVICIO DE MANTENIMIENTO

## Matriz de relaciones

| Relación                     | Entidad 1 | Cardinalidad | Participación | Entidad 2                 | Cardinalidad | Participación |
| ------------------------------- | ----------- | -------------- | ---------------- | --------------------------- | -------------- | ---------------- |
| ASIGNA / ESTÁ ASIGNADO A     | OFICINA   | (0,N)        | Opcional       | VEHÍCULO                 | (1,1)        | Obligatoria    |
| REALIZA / ES REALIZADO POR    | CLIENTE   | (0,N)        | Opcional       | ALQUILER                  | (1,1)        | Obligatoria    |
| SE ALQUILA EN / CORRESPONDE A | VEHÍCULO | (0,N)        | Opcional       | ALQUILER                  | (1,1)        | Obligatoria    |
| RECIBE / SE REALIZA A         | VEHÍCULO | (0,N)        | Opcional       | SERVICIO DE MANTENIMIENTO | (0,N)        | Opcional       |

## Mermaid

```mermaid
flowchart LR
    VEHICULO["VEHÍCULO"]
    OFICINA["OFICINA"]
    CLIENTE["CLIENTE"]
    ALQUILER["ALQUILER"]
    SERVICIO["SERVICIO DE MANTENIMIENTO"]

    ASIGNADO{"ASIGNA / ESTÁ ASIGNADO A"}
    REALIZA{"REALIZA / ES REALIZADO POR"}
    CORRESPONDE{"SE ALQUILA EN / CORRESPONDE A"}
    RECIBE{"RECIBE / SE REALIZA A"}

    MATRICULA(("matrícula"))
    MODELO(("modelo"))
    ID_O(("identificador"))
    DIRECCION(("dirección"))
    FECHA_I(("fecha de inicio"))
    FECHA_F(("fecha de fin"))
    ID_S(("identificador"))
    DESC_S(("descripción"))

    VEHICULO --- MATRICULA
    VEHICULO --- MODELO
    OFICINA --- ID_O
    OFICINA --- DIRECCION
    ALQUILER --- FECHA_I
    ALQUILER --- FECHA_F
    SERVICIO --- ID_S
    SERVICIO --- DESC_S

    OFICINA ---|"0..N"| ASIGNADO
    ASIGNADO ---|"1..1"| VEHICULO
    CLIENTE ---|"0..N"| REALIZA
    REALIZA ---|"1..1"| ALQUILER
    VEHICULO ---|"0..N"| CORRESPONDE
    CORRESPONDE ---|"1..1"| ALQUILER
    VEHICULO ---|"0..N"| RECIBE
    RECIBE ---|"0..N"| SERVICIO
```

# Variante v6 — Tienda en línea

## Entidades

CATEGORÍA, PRODUCTO, CLIENTE, PEDIDO

## Matriz de relaciones

| Relación                    | Entidad 1  | Cardinalidad | Participación | Entidad 2 | Cardinalidad | Participación |
| ------------------------------ | ------------ | -------------- | ---------------- | ----------- | -------------- | ---------------- |
| AGRUPA / PERTENECE A         | CATEGORÍA | (0,N)        | Opcional       | PRODUCTO  | (1,1)        | Obligatoria    |
| REALIZA / ES REALIZADO POR   | CLIENTE    | (0,N)        | Opcional       | PEDIDO    | (1,1)        | Obligatoria    |
| CONTIENE / ESTÁ INCLUIDO EN | PEDIDO     | (1,N)        | Obligatoria    | PRODUCTO  | (0,N)        | Opcional       |

## Mermaid

```mermaid
flowchart LR
    CATEGORIA["CATEGORÍA"]
    PRODUCTO["PRODUCTO"]
    CLIENTE["CLIENTE"]
    PEDIDO["PEDIDO"]

    INCLUYE{"AGRUPA / PERTENECE A"}
    REALIZA{"REALIZA / ES REALIZADO POR"}
    CONTIENE{"CONTIENE / ESTÁ INCLUIDO EN"}

    ID_C(("identificador"))
    NOM_C(("nombre"))
    ID_P(("identificador"))
    NOM_P(("nombre"))
    FECHA(("fecha"))
    ESTADO(("estado"))
    CANTIDAD(("cantidad solicitada"))

    CATEGORIA --- ID_C
    CATEGORIA --- NOM_C
    PRODUCTO --- ID_P
    PRODUCTO --- NOM_P
    PEDIDO --- FECHA
    PEDIDO --- ESTADO

    CATEGORIA ---|"0..N"| INCLUYE
    INCLUYE ---|"1..1"| PRODUCTO
    CLIENTE ---|"0..N"| REALIZA
    REALIZA ---|"1..1"| PEDIDO
    PEDIDO ---|"1..N"| CONTIENE
    CONTIENE ---|"0..N"| PRODUCTO
    CONTIENE --- CANTIDAD
```

# Variante v7 — Organización de eventos

## Entidades

EVENTO, SALA, EMPLEADO, ASISTENTE, INSCRIPCIÓN

## Matriz de relaciones

| Relación                                    | Entidad 1 | Cardinalidad | Participación | Entidad 2    | Cardinalidad | Participación |
| ---------------------------------------------- | ----------- | -------------- | ---------------- | -------------- | -------------- | ---------------- |
| ALOJA / SE CELEBRA EN                        | SALA      | (0,N)        | Opcional       | EVENTO       | (1,1)        | Obligatoria    |
| COLABORA EN / CUENTA CON LA COLABORACIÓN DE | EMPLEADO  | (0,N)        | Opcional       | EVENTO       | (0,N)        | Opcional       |
| SE INSCRIBE EN / RECIBE LA INSCRIPCIÓN DE   | ASISTENTE | (0,N)        | Opcional       | INSCRIPCIÓN | (1,1)        | Obligatoria    |
| INCLUYE / CORRESPONDE A                      | EVENTO    | (0,N)        | Opcional       | INSCRIPCIÓN | (1,1)        | Obligatoria    |

## Mermaid

```mermaid
flowchart LR
    EVENTO["EVENTO"]
    SALA["SALA"]
    EMPLEADO["EMPLEADO"]
    ASISTENTE["ASISTENTE"]
    INSCRIPCION["INSCRIPCIÓN"]

    CELEBRA{"ALOJA / SE CELEBRA EN"}
    COLABORA{"COLABORA EN / CUENTA CON LA COLABORACIÓN DE"}
    SE_INSCRIBE{"SE INSCRIBE EN / RECIBE LA INSCRIPCIÓN DE"}
    CORRESPONDE{"INCLUYE / CORRESPONDE A"}

    ID_E(("identificador"))
    NOM_E(("nombre"))
    FECHA_E(("fecha"))
    ID_S(("identificador"))
    NOM_S(("nombre"))
    FUNCION(("función desempeñada"))
    FECHA_I(("fecha"))
    ESTADO(("estado"))

    EVENTO --- ID_E
    EVENTO --- NOM_E
    EVENTO --- FECHA_E
    SALA --- ID_S
    SALA --- NOM_S
    COLABORA --- FUNCION
    INSCRIPCION --- FECHA_I
    INSCRIPCION --- ESTADO

    SALA ---|"0..N"| CELEBRA
    CELEBRA ---|"1..1"| EVENTO
    EMPLEADO ---|"0..N"| COLABORA
    COLABORA ---|"0..N"| EVENTO
    ASISTENTE ---|"0..N"| SE_INSCRIBE
    SE_INSCRIBE ---|"1..1"| INSCRIPCION
    EVENTO ---|"0..N"| CORRESPONDE
    CORRESPONDE ---|"1..1"| INSCRIPCION
```

# Variante v8 — Empresa de transporte

## Entidades

RUTA, SERVICIO, CONDUCTOR, VEHÍCULO, CLIENTE, BILLETE

## Matriz de relaciones

| Relación                  | Entidad 1 | Cardinalidad | Participación | Entidad 2 | Cardinalidad | Participación |
| ---------------------------- | ----------- | -------------- | ---------------- | ----------- | -------------- | ---------------- |
| OFRECE / SIGUE             | RUTA      | (0,N)        | Opcional       | SERVICIO  | (1,1)        | Obligatoria    |
| CONDUCE / ES CONDUCIDO POR | CONDUCTOR | (0,N)        | Opcional       | SERVICIO  | (1,1)        | Obligatoria    |
| UTILIZA / ES UTILIZADO POR | VEHÍCULO | (0,N)        | Opcional       | SERVICIO  | (1,1)        | Obligatoria    |
| COMPRA / ES COMPRADO POR   | CLIENTE   | (0,N)        | Opcional       | BILLETE   | (1,1)        | Obligatoria    |
| INCLUYE / CORRESPONDE A    | SERVICIO  | (0,N)        | Opcional       | BILLETE   | (1,1)        | Obligatoria    |

## Mermaid

```mermaid
flowchart LR
    RUTA["RUTA"]
    SERVICIO["SERVICIO"]
    CONDUCTOR["CONDUCTOR"]
    VEHICULO["VEHÍCULO"]
    CLIENTE["CLIENTE"]
    BILLETE["BILLETE"]

    CORRESPONDE_R{"OFRECE / SIGUE"}
    REALIZA{"CONDUCE / ES CONDUCIDO POR"}
    UTILIZA{"UTILIZA / ES UTILIZADO POR"}
    COMPRA{"COMPRA / ES COMPRADO POR"}
    CORRESPONDE_B{"INCLUYE / CORRESPONDE A"}

    ID_R(("identificador"))
    ORIGEN(("origen"))
    DESTINO(("destino"))
    FECHA(("fecha"))
    HORA(("hora de salida"))
    COD_C(("código"))
    NOM_C(("nombre"))
    MATRICULA(("matrícula"))
    MODELO(("modelo"))
    PRECIO(("precio"))
    FECHA_C(("fecha de compra"))

    RUTA --- ID_R
    RUTA --- ORIGEN
    RUTA --- DESTINO
    SERVICIO --- FECHA
    SERVICIO --- HORA
    CONDUCTOR --- COD_C
    CONDUCTOR --- NOM_C
    VEHICULO --- MATRICULA
    VEHICULO --- MODELO
    BILLETE --- PRECIO
    BILLETE --- FECHA_C

    RUTA ---|"0..N"| CORRESPONDE_R
    CORRESPONDE_R ---|"1..1"| SERVICIO
    CONDUCTOR ---|"0..N"| REALIZA
    REALIZA ---|"1..1"| SERVICIO
    VEHICULO ---|"0..N"| UTILIZA
    UTILIZA ---|"1..1"| SERVICIO
    CLIENTE ---|"0..N"| COMPRA
    COMPRA ---|"1..1"| BILLETE
    SERVICIO ---|"0..N"| CORRESPONDE_B
    CORRESPONDE_B ---|"1..1"| BILLETE
```

# Variante v9 — Museo

## Entidades

OBRA, SALA, ARTISTA, VISITANTE, RESERVA, VISITA GUIADA

## Matriz de relaciones

| Relación                     | Entidad 1     | Cardinalidad | Participación | Entidad 2 | Cardinalidad | Participación |
| ------------------------------- | --------------- | -------------- | ---------------- | ----------- | -------------- | ---------------- |
| ALBERGA / SE EXPONE EN        | SALA          | (0,N)        | Opcional       | OBRA      | (1,1)        | Obligatoria    |
| CREA / ES CREADA POR          | ARTISTA       | (0,N)        | Opcional       | OBRA      | (0,N)        | Opcional       |
| REALIZA / ES REALIZADA POR    | VISITANTE     | (0,N)        | Opcional       | RESERVA   | (1,1)        | Obligatoria    |
| SE RESERVA MEDIANTE / RESERVA | VISITA GUIADA | (0,N)        | Opcional       | RESERVA   | (1,1)        | Obligatoria    |

## Mermaid

```mermaid
flowchart LR
    OBRA["OBRA"]
    SALA["SALA"]
    ARTISTA["ARTISTA"]
    VISITANTE["VISITANTE"]
    RESERVA["RESERVA"]
    VISITA["VISITA GUIADA"]

    EXPONE{"ALBERGA / SE EXPONE EN"}
    CREA{"CREA / ES CREADA POR"}
    REALIZA{"REALIZA / ES REALIZADA POR"}
    CORRESPONDE{"SE RESERVA MEDIANTE / RESERVA"}

    ID_O(("identificador"))
    TITULO(("título"))
    ID_S(("identificador"))
    NOM_S(("nombre"))
    ID_A(("identificador"))
    NOM_A(("nombre"))
    FECHA(("fecha"))
    ASISTENTES(("número de asistentes"))
    ID_V(("identificador"))
    DURACION(("duración"))

    OBRA --- ID_O
    OBRA --- TITULO
    SALA --- ID_S
    SALA --- NOM_S
    ARTISTA --- ID_A
    ARTISTA --- NOM_A
    RESERVA --- FECHA
    RESERVA --- ASISTENTES
    VISITA --- ID_V
    VISITA --- DURACION

    SALA ---|"0..N"| EXPONE
    EXPONE ---|"1..1"| OBRA
    ARTISTA ---|"0..N"| CREA
    CREA ---|"0..N"| OBRA
    VISITANTE ---|"0..N"| REALIZA
    REALIZA ---|"1..1"| RESERVA
    VISITA ---|"0..N"| CORRESPONDE
    CORRESPONDE ---|"1..1"| RESERVA
```

# Variante v10 — Empresa de desarrollo

## Entidades

DEPARTAMENTO, PROYECTO, EMPLEADO, TAREA

## Matriz de relaciones

| Relación               | Entidad 1    | Cardinalidad | Participación | Entidad 2 | Cardinalidad | Participación |
| ------------------------- | -------------- | -------------- | ---------------- | ----------- | -------------- | ---------------- |
| GESTIONA / PERTENECE A  | DEPARTAMENTO | (0,N)        | Opcional       | PROYECTO  | (1,1)        | Obligatoria    |
| TRABAJA EN / CUENTA CON | EMPLEADO     | (0,N)        | Opcional       | PROYECTO  | (0,N)        | Opcional       |
| INCLUYE / PERTENECE A   | PROYECTO     | (0,N)        | Opcional       | TAREA     | (1,1)        | Obligatoria    |

## Mermaid

```mermaid
flowchart LR
    DEPARTAMENTO["DEPARTAMENTO"]
    PROYECTO["PROYECTO"]
    EMPLEADO["EMPLEADO"]
    TAREA["TAREA"]

    TIENE{"GESTIONA / PERTENECE A"}
    TRABAJA{"TRABAJA EN / CUENTA CON"}
    INCLUYE{"INCLUYE / PERTENECE A"}

    ID_D(("identificador"))
    NOM_D(("nombre"))
    ID_P(("identificador"))
    NOM_P(("nombre"))
    FECHA(("fecha de incorporación"))
    PORCENTAJE(("porcentaje de dedicación"))
    DESC_T(("descripción"))
    PRIORIDAD(("prioridad"))

    DEPARTAMENTO --- ID_D
    DEPARTAMENTO --- NOM_D
    PROYECTO --- ID_P
    PROYECTO --- NOM_P
    TRABAJA --- FECHA
    TRABAJA --- PORCENTAJE
    TAREA --- DESC_T
    TAREA --- PRIORIDAD

    DEPARTAMENTO ---|"0..N"| TIENE
    TIENE ---|"1..1"| PROYECTO
    EMPLEADO ---|"0..N"| TRABAJA
    TRABAJA ---|"0..N"| PROYECTO
    PROYECTO ---|"0..N"| INCLUYE
    INCLUYE ---|"1..1"| TAREA
```

