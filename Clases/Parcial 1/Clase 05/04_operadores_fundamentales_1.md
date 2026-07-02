## Operadores Fundamentales

El conjunto de operadores del álgebra relacional está compuesto por un grupo de operaciones denominadas **fundamentales**, que forman un conjunto completo en el sentido de que cualquier consulta relacional puede expresarse utilizando únicamente estas operaciones.
Estos operadores son selección, proyección, unión, diferencia, producto cartesiano y renombramiento.

### La **selección**

Representada por σ, permite filtrar tuplas de una relación que satisfacen una condición booleana.
Por ejemplo, σ salario > 3000 (EMPLEADO) devuelve el subconjunto de la relación EMPLEADO cuyas tuplas tienen un salario mayor a 3000.
La selección es conmutativa, es decir, se pueden aplicar varias condiciones en cualquier orden obteniendo el mismo resultado, y también se puede descomponer una condición compleja en varias más simples aplicadas secuencialmente.

**Relación EMPLEADO**

| ID | NOMBRE | DEPARTAMENTO | SALARIO |
|----|--------|---------|---------|
| 1  | Ana    | IT      | 4000    |
| 2  | Luis   | Ventas  | 3200    |
| 3  | Marta  | IT      | 2800    |

**Operación:** σ DEPARTAMENTO = "IT" (EMPLEADO)

**Resultado:**

| ID | NOMBRE | DEPARTAMENTO | SALARIO |
|----|--------|---------|---------|
| 1  | Ana    | IT      | 4000    |
| 3  | Marta  | IT      | 2800    |

### La **proyección**

Representada por π, permite seleccionar un subconjunto de atributos de una relación.
El resultado es una nueva relación que contiene solo las columnas especificadas y no incluye duplicados, ya que el resultado debe seguir siendo un conjunto.
Por ejemplo, π nombre, salario (EMPLEADO) genera una relación con únicamente los atributos nombre y salario de EMPLEADO.
Proyección y selección suelen emplearse juntas: primero se filtran las tuplas con σ y luego se extraen las columnas deseadas con π.

**Operación:** π NOMBRE, DEPARTAMENTO (σ DEPARTAMENTO ="IT"(EMPLEADO))

| NOMBRE | DEPARTAMENTO |
|--------|---------|
| Ana    | IT      |
| Marta  | IT      |

### La **unión**

Denotada por ∪, combina las tuplas de dos relaciones y devuelve una nueva relación que contiene todas las tuplas que aparecen en alguna de ellas, eliminando duplicados.
Para que la unión esté bien definida, las dos relaciones deben ser **compatibles para unión**, lo que significa que deben tener el mismo número de atributos y que los atributos correspondientes deben ser del mismo dominio.

**Relación R1: CLIENTES_2023**

| ID | NOMBRE |
|----|--------|
| 1  | Ana    |
| 2  | Luis   |

**Relación R2: CLIENTES_2024**

| ID | NOMBRE |
|----|--------|
| 3  | Marta  |
| 4  | Jorge  |

**Resultado R1 ∪ R2**

| ID | NOMBRE |
|----|--------|
| 1  | Ana    |
| 2  | Luis   |
| 3  | Marta  |
| 4  | Jorge  |

