# Refuerzo de Relaciones Entre Entidades

En el diseño conceptual, las relaciones describen **cómo se asocian las entidades**.
Debemos analizar **dos cosas** en cada relación:

1. **Cardinalidad** → cuántas ocurrencias de una entidad se pueden asociar con otra.
2. **Opcionalidad** → si la relación es obligatoria o puede no existir (0..1, 0..N).

---

## 1. Relación 1 a 1 (1:1)

**Definición:**
Cada ocurrencia de la entidad A está asociada con **a lo sumo una** ocurrencia de la entidad B, y viceversa.

**Ejemplo:**

- **Persona** ↔ **Pasaporte**
- *Una persona posee un único pasaporte vigente*
- *Un pasaporte pertenece a una sola persona*

**Representación bidireccional:**

- **Persona —(posee)→ Pasaporte**
- **Pasaporte —(pertenece a)→ Persona**

**Cardinalidad:**
1:1

---

## 2. Relación 1 a N (1:N)

**Definición:**
Una ocurrencia de A puede estar relacionada con **muchas** ocurrencias de B,
pero cada ocurrencia de B está asociada con **exactamente una** ocurrencia de A.

**Ejemplo:**

- **Departamento** ↔ **Empleado**
- *Un departamento tiene muchos empleados*
- *Un empleado pertenece a un único departamento*

**Representación bidireccional:**

- **Departamento —(tiene)→ Empleado (N)**
- **Empleado —(pertenece a)→ Departamento (1)**

**Cardinalidad:**
1:N

---

## 3. Relación N a M (N:M)

**Definición:**
Una ocurrencia de A puede relacionarse con muchas de B y viceversa.
Se implementa normalmente con **tabla intermedia** (entidad débil o relación con atributos).

**Ejemplo:**

- **Estudiante** ↔ **Materia**
- *Un estudiante cursa muchas materias*
- *Una materia es cursada por muchos estudiantes*

**Representación bidireccional:**

- **Estudiante —(cursa)→ Materia (M)**
- **Materia —(es cursada por)→ Estudiante (N)**

**Cardinalidad:**
N:M

---

## 4. Relaciones Opcionales (0..1, 0..N)

Cuando una relación **puede no existir**, se agrega el rango mínimo 0.

### 4.1. Relación 0..1 a 1

**Ejemplo:**
**Empleado** ↔ **AutoAsignado**

- *Un empleado puede o no tener un auto asignado*
- *Si el auto existe, pertenece exactamente a un empleado*

**Cardinalidad:**
0..1 : 1

**Bidireccionalidad:**

- **Empleado —(puede tener)→ AutoAsignado (0..1)**
- **AutoAsignado —(es de)→ Empleado (1)**

---

### 4.2. Relación 0..1 a N

**Ejemplo:**
**Cliente** ↔ **Pedido**

- *Un cliente puede o no haber hecho pedidos*
- *Un pedido siempre está asociado a un cliente*

**Cardinalidad:**
0..1 : N

**Bidireccionalidad:**

- **Cliente —(realiza)→ Pedido (0..N)**
- **Pedido —(pertenece a)→ Cliente (1)**

---

### 4.3. Relación 0..N a N..M

**Ejemplo:**
**Profesor** ↔ **ProyectoInvestigación**

- *Un profesor puede no participar en ningún proyecto o en varios*
- *Un proyecto puede no tener profesores asignados aún, o tener varios*

**Cardinalidad:**
0..N : 0..M

**Bidireccionalidad:**

- **Profesor —(participa en)→ ProyectoInvestigación (0..M)**
- **ProyectoInvestigación —(tiene participante)→ Profesor (0..N)**
  

