# Ejercicios Resueltos – Operadores Renombramiento (ρ) y Producto Cartesiano (×)

## Relación de Ejemplo

**EMPLEADO**

| id_empleado | nombre      | departamento | salario |
|-------------|-------------|--------|--------|
| 1           | Ana López   | Ventas | 1500   |
| 2           | Juan Pérez  | IT     | 2500   |
| 3           | Marta Ruiz  | IT     | 1800   |
| 4           | Pedro León  | HR     | 1200   |
| 5           | Carla Díaz  | IT     | 3000   |

**DEPARTAMENTO**

| id_depto | nombre_departamento  |
|---------|---------------|
| D1      | Ventas        |
| D2      | IT            |
| D3      | HR            |

---

## Operador Renombramiento (ρ)

El renombramiento permite cambiar el nombre de una relación o de sus atributos para facilitar operaciones posteriores.

**Ejercicio 1 – Fácil**

Objetivo: Renombrar la relación EMPLEADO como EMP.

Operación:

ρ(EMP)(EMPLEADO)

Resultado (mismos datos, nuevo nombre de la relación):

| id_empleado | nombre      | departamento | salario |
|-------------|-------------|--------|--------|
| 1           | Ana López   | Ventas | 1500   |
| 2           | Juan Pérez  | IT     | 2500   |
| 3           | Marta Ruiz  | IT     | 1800   |
| 4           | Pedro León  | HR     | 1200   |
| 5           | Carla Díaz  | IT     | 3000   |

---

**Ejercicio 2 – Medio**

Objetivo: Renombrar atributos para uniformidad: id_empleado → id, nombre → nombre_emp.

Operación:

ρ((id, nombre_emp, departamento , salario))(EMPLEADO)

Resultado:

| id | nombre_emp | departamento | salario |
|----|-------------|--------|--------|
| 1  | Ana López   | Ventas | 1500   |
| 2  | Juan Pérez  | IT     | 2500   |
| 3  | Marta Ruiz  | IT     | 1800   |
| 4  | Pedro León  | HR     | 1200   |
| 5  | Carla Díaz  | IT     | 3000   |

---

**Ejercicio 3 – Difícil**

Objetivo: Renombrar una relación para evitar colisión de nombres antes de un producto cartesiano.

Operación:

ρ(E1)(EMPLEADO) × ρ(E2)(EMPLEADO)]

Resultado (parcial, mostrando solo 3 filas):

| E1.id_empleado | E1.nombre   | E1.departamento | E1.salario | E2.id_empleado | E2.nombre    | E2.departamento | E2.salario |
|----------------|-------------|----------|-----------|----------------|-------------|---------|-----------|
| 1              | Ana López   | Ventas   | 1500      | 1              | Ana López   | Ventas  | 1500      |
| 1              | Ana López   | Ventas   | 1500      | 2              | Juan Pérez  | IT      | 2500      |
| 1              | Ana López   | Ventas   | 1500      | 3              | Marta Ruiz  | IT      | 1800      |
| ...            | ...         | ...      | ...       | ...            | ...         | ...     | ...       |

---

## Operador Producto Cartesiano (×)

El producto cartesiano combina todas las tuplas de dos relaciones. Puede ser costoso en la práctica, pero es la base de las operaciones de JOIN.

**Ejercicio 1 – Fácil**

Objetivo: Combinar todos los empleados con todos los departamentos (sin condición).

Operación:

EMPLEADO × DEPARTAMENTO

Resultado (parcial):

| id_empleado | nombre      | depto  | salario | id_depto | nombre_departamento |
|-------------|-------------|--------|--------|---------|-------------|
| 1           | Ana López   | Ventas | 1500   | D1      | Ventas      |
| 1           | Ana López   | Ventas | 1500   | D2      | IT          |
| 1           | Ana López   | Ventas | 1500   | D3      | HR          |
| 2           | Juan Pérez  | IT     | 2500   | D1      | Ventas      |
| ...         | ...         | ...    | ...    | ...     | ...         |

---

**Ejercicio 2 – Medio**

Objetivo: Hacer producto cartesiano pero solo mostrar id_empleado, nombre, nombre_departamento.

Operación:

π(id_empleado, nombre, nombre_departamento)(EMPLEADO × DEPARTAMENTO)

Resultado (parcial):

| id_empleado | nombre      | nombre_departamento |
|-------------|-------------|-------------|
| 1           | Ana López   | Ventas      |
| 1           | Ana López   | IT          |
| 1           | Ana López   | HR          |
| 2           | Juan Pérez  | Ventas      |
| ...         | ...         | ...         |

---

**Ejercicio 3 – Difícil**

Objetivo: Usar producto cartesiano y luego selección para hacer un "JOIN" manual: obtener solo los empleados cuyo departamento coincide con nombre_departamento.

Operación:

σ(departamento = nombre_departamento)(EMPLEADO × DEPARTAMENTO)

Resultado:

| id_empleado | nombre      | depto  | salario | id_departamento | nombre_departamento |
|-------------|-------------|--------|--------|---------|-------------|
| 1           | Ana López   | Ventas | 1500   | D1      | Ventas      |
| 2           | Juan Pérez  | IT     | 2500   | D2      | IT          |
| 3           | Marta Ruiz  | IT     | 1800   | D2      | IT          |
| 4           | Pedro León  | HR     | 1200   | D3      | HR          |
| 5           | Carla Díaz  | IT     | 3000   | D2      | IT          |

