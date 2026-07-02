## Ejercicio 1: Plataforma para empresa de servicios


Una **empresa de servicios** quiere un sistema para registrar sus operaciones.
Nos entregan los siguientes requerimientos:

- La empresa ofrece **servicios** de diferentes tipos.
- Los **clientes** contratan uno o varios servicios.
- Cada contratación se registra como un **contrato** con fecha de inicio y fin.
- Los contratos son atendidos por **empleados**, que pueden ser de tipo **Técnico** o **Administrativo**.
- Cada empleado puede atender muchos contratos, pero un contrato solo es atendido por un empleado.
- Los clientes pueden ser **Personas** o **Empresas** (hay que modelar esta diferencia).
- Se desea conocer qué servicios se han contratado, por quién y quién los atendió.

---

## Paso 1 – Identificación de Entidades

Entidades detectadas:

- **Cliente** (superclase)
- **Persona** (subclase)
- **Empresa** (subclase)
- **Servicio**
- **Contrato**
- **Empleado** (superclase)
- **Técnico** (subclase)
- **Administrativo** (subclase)

---

## Paso 2 – Relaciones y Verbos

Definimos las relaciones entre entidades usando verbos claros y cardinalidades:

- **Cliente —< Contrata >— Contrato**
  
  - Un cliente **puede contratar** muchos contratos (1:N).
  - Un contrato **pertenece** a un solo cliente (N:1).
- **Contrato —< Incluye >— Servicio**
  
  - Un contrato **puede incluir** varios servicios (1:N).
  - Un servicio **puede estar incluido en** varios contratos (N:M).
- **Empleado —< Atiende >— Contrato**
  
  - Un empleado **atiende** muchos contratos (1:N).
  - Un contrato **es atendido por** un solo empleado (N:1).

---

## Paso 3 – Atributos (Nivel Conceptual)

- **Cliente**: id_cliente, nombre, dirección, teléfono
- **Persona**: fecha_nacimiento, DNI
- **Empresa**: razón_social, CIF
- **Servicio**: id_servicio, nombre, tipo, precio
- **Contrato**: id_contrato, fecha_inicio, fecha_fin, estado
- **Empleado**: id_empleado, nombre, cargo
- **Técnico**: especialidad
- **Administrativo**: departamento

---

## Paso 4 – Identificadores

Identificamos los **atributos identificadores** (únicos) de cada entidad.
En diseño conceptual solo marcamos cuáles son **identificadores**, no definimos su tipo:

- Cliente: **id_cliente**
- Servicio: **id_servicio**
- Contrato: **id_contrato**
- Empleado: **id_empleado**

---

## Paso 5 – Jerarquías de Generalización

Definimos jerarquías donde aplica:

Cliente
├── Persona
└── Empresa

Empleado
├── Técnico
└── Administrativo

- **Restricción de cobertura:** Total (todo cliente es persona o empresa).
- **Restricción de disyunción:** Disjunta (no puede ser ambas).
- Para empleados, también es total y disjunta.

```

```

