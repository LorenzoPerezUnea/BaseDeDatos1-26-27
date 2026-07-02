## Operadores Fundamentales

### La **diferencia**

Denotada por −, devuelve las tuplas que aparecen en la primera relación pero no en la segunda, y también requiere compatibilidad de atributos.
Por ejemplo, CLIENTES_TOTALES − CLIENTES_MOROSOS devolvería los clientes que no están en la lista de morosos.
Unión y diferencia permiten realizar operaciones de conjuntos de forma directa sobre los datos.

**Relación R1**

| ID | NOMBRE |
|----|--------|
| 1  | Ana    |
| 2  | Luis   |
| 3  | Marta  |
| 4  | Jorge  |

**Relación R2**

| ID | NOMBRE |
|----|--------|
| 3  | Marta  |
| 4  | Jorge  |

**Resultado R1 − R2**

| ID | NOMBRE |
|----|--------|
| 1  | Ana    |
| 2  | Luis   |

### El **producto cartesiano**

Representado por ×, genera todas las combinaciones posibles de tuplas de dos relaciones.
Si R tiene n tuplas y S tiene m tuplas, el resultado tiene n × m tuplas y contiene todos los atributos de R y de S.
Aunque el resultado puede ser muy grande, esta operación es esencial porque constituye el primer paso para formar **joins**: normalmente se aplica una selección sobre el producto para quedarse únicamente con las combinaciones que cumplen una condición.

**Relación CLIENTE**

| ID | NOMBRE |
|----|--------|
| 1  | Ana    |
| 2  | Luis   |

**Relación PEDIDO**

| IDP | IMPORTE |
|-----|---------|
| A   | 100     |
| B   | 250     |

**Resultado CLIENTE × PEDIDO**

| ID | NOMBRE | IDP | IMPORTE |
|----|--------|-----|---------|
| 1  | Ana    | A   | 100     |
| 1  | Ana    | B   | 250     |
| 2  | Luis   | A   | 100     |
| 2  | Luis   | B   | 250     |

### El **renombramiento**

Denotado por ρ, permite asignar un nuevo nombre a la relación o a los atributos de la relación.
Esta operación es necesaria para desambiguar nombres cuando se trabaja con varias relaciones que comparten atributos con el mismo nombre, o cuando se necesita combinar una relación consigo misma.
Por ejemplo, ρ EMP(id, nombre, depto, salario) (EMPLEADO) produce una relación con los mismos datos pero renombrada EMP.

**Relación EMPLEADO**

| ID | NOMBRE | DEPTO | SALARIO |
|----|--------|-------|---------|
| 1  | Ana    | IT    | 4000    |
| 2  | Luis   | Ventas| 3200    |

**Operación:**
ρ EMP(ID, NOMBRE, DEPTO, SAL) (EMPLEADO)

**Resultado:**
La relación sigue teniendo las mismas tuplas, pero ahora se llama `EMP` y el último atributo se llama `SAL` en lugar de `SALARIO`.

| ID | NOMBRE | DEPTO | SAL |
|----|--------|-------|-----|
| 1  | Ana    | IT    | 4000|
| 2  | Luis   | Ventas| 3200|

