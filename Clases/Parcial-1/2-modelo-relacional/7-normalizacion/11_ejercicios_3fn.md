# Ejercicios 3FN

Una vez comprendido el concepto de dependencia transitiva, resulta mucho más sencillo reconocer cuándo una tabla necesita alcanzar la Tercera Forma Normal.

### Ejercicio 1

Analiza la siguiente tabla.

| IdEmpleado | Nombre | IdDepartamento | NombreDepartamento |
| ------------ | -------- | ---------------- | -------------------- |

Las dependencias funcionales son:

```text
IdEmpleado → Nombre

IdEmpleado → IdDepartamento

IdDepartamento → NombreDepartamento
```

**Preguntas**

1. ¿Cumple la Tercera Forma Normal?
2. ¿Qué dependencia transitiva existe?
3. ¿Cómo reorganizarías las tablas?

### Solución

No cumple la 3FN.

Existe la dependencia:

```text
IdDepartamento → NombreDepartamento
```

La solución consiste en crear una tabla independiente.

```text
DEPARTAMENTO

IdDepartamento
NombreDepartamento
```

```text
EMPLEADO

IdEmpleado
Nombre
IdDepartamento
```

---

### Ejercicio 2

Analiza la siguiente tabla.

| IdCliente | Nombre | Dirección |
| ----------: | -------- | ------------ |

Las dependencias son:

```text
IdCliente → Nombre

IdCliente → Dirección
```

### Solución

Sí cumple la Tercera Forma Normal.

Todos los atributos dependen directamente de la clave primaria.

No existen dependencias transitivas.

---

### Ejercicio 3

Una tienda almacena esta información.

| Producto | Categoría | ResponsableCategoría |

Se conocen las dependencias:

```text
Producto → Categoría

Categoría → ResponsableCategoría
```

### Pregunta

¿Cumple la 3FN?

### Solución

No.

Existe una dependencia transitiva.

El responsable depende de la categoría y no directamente del producto.

Debe crearse una tabla independiente para las categorías.

### Ideas clave

* La clave para detectar la 3FN consiste en buscar dependencias entre atributos no clave.
* Las dependencias transitivas generan redundancia.
* Separar entidades elimina estas dependencias.
* La práctica facilita reconocer rápidamente estos patrones.
* La 3FN representa el nivel de normalización más habitual en aplicaciones empresariales.

