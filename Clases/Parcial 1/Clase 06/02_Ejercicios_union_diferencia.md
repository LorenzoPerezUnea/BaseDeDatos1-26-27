# Ejercicios Resueltos – Operadores Unión (∪) y Diferencia (−)

## Relaciones de Ejemplo

Ambas relaciones tienen el mismo esquema (mismos atributos), requisito para aplicar **Unión** y **Diferencia**.

**EMPLEADO_A**

| id_empleado | nombre      | departamento |
|-------------|-------------|--------|
| 1           | Ana López   | Ventas |
| 2           | Juan Pérez  | IT     |
| 3           | Marta Ruiz  | IT     |

**EMPLEADO_B**

| id_empleado | nombre       | departamento |
|-------------|--------------|--------|
| 3           | Marta Ruiz   | IT     |
| 4           | Pedro León   | HR     |
| 5           | Carla Díaz   | IT     |

---

## Operador Unión (∪)

La unión combina tuplas de dos relaciones eliminando duplicados (por definición en álgebra relacional, se asume *SET UNION*).

**Ejercicio 1 – Fácil**

Objetivo: Obtener todos los empleados de A o B (sin repetidos).
Operación:

EMPLEADO_A ∪ cup EMPLEADO_B

Resultado:

| id_empleado | nombre      | departamento |
|-------------|-------------|--------|
| 1           | Ana López   | Ventas |
| 2           | Juan Pérez  | IT     |
| 3           | Marta Ruiz  | IT     |
| 4           | Pedro León  | HR     |
| 5           | Carla Díaz  | IT     |

---

**Ejercicio 2 – Medio**

Objetivo: Obtener la lista de nombres de empleados de A o B, mostrando solo el atributo **nombre**.

Operación:

π(nombre)(EMPLEADO_A) ∪ π(nombre)(EMPLEADO_B)

Resultado:

| nombre      |
|-------------|
| Ana López   |
| Juan Pérez  |
| Marta Ruiz  |
| Pedro León  |
| Carla Díaz  |

---

**Ejercicio 3 – Difícil**

Objetivo: Obtener la unión de empleados de A y B, pero renombrando para que el resultado se llame TODOS_EMPLEADOS.

Operación:

ρ(TODOS_EMPLEADOS)(EMPLEADO_A ∪ EMPLEADO_B)

Resultado (relación renombrada):

**TODOS_EMPLEADOS**

| id_empleado | nombre      | departamento |
|-------------|-------------|--------|
| 1           | Ana López   | Ventas |
| 2           | Juan Pérez  | IT     |
| 3           | Marta Ruiz  | IT     |
| 4           | Pedro León  | HR     |
| 5           | Carla Díaz  | IT     |

---

## Operador Diferencia (−)

La diferencia obtiene tuplas que están en la primera relación pero no en la segunda.

**Ejercicio 1 – Fácil**

Objetivo: Obtener los empleados que están en A pero no en B.

Operación:

EMPLEADO_A - EMPLEADO_B

Resultado:

| id_empleado | nombre      | departamento |
|-------------|-------------|--------|
| 1           | Ana López   | Ventas |
| 2           | Juan Pérez  | IT     |

---

**Ejercicio 2 – Medio**

Objetivo: Obtener solo los **nombres** de los empleados exclusivos de A (no presentes en B).

Operación:

π(nombre)(EMPLEADO_A) - π(nombre)(EMPLEADO_B)

Resultado:

| nombre      |
|-------------|
| Ana López   |
| Juan Pérez  |

---

**Ejercicio 3 – Difícil**

Objetivo: Obtener empleados que están en A pero no en B y luego renombrar la relación como EMPLEADOS_EXCLUSIVOS.

Operación:

ρ(EMPLEADOS_EXCLUSIVOS)(EMPLEADO_A - EMPLEADO_B)

Resultado:

**EMPLEADOS_EXCLUSIVOS**

| id_empleado | nombre      | departamento |
|-------------|-------------|--------|
| 1           | Ana López   | Ventas |
| 2           | Juan Pérez  | IT     |

