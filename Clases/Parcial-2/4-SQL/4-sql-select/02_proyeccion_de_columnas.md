# Proyección de columnas

## Introducción

En el apartado anterior aprendimos que la consulta más sencilla en SQL consiste en utilizar:

```sql
SELECT *
FROM Tabla;
```

El carácter `*` indica que queremos recuperar **todas las columnas** de la tabla.

Aunque esta forma resulta muy útil para comenzar a aprender SQL y para inspeccionar rápidamente una tabla, en aplicaciones reales rara vez es la mejor opción.

En la mayoría de los casos únicamente necesitamos una parte de la información.

Por ejemplo:

* una lista de nombres de clientes;
* los precios de los productos;
* los correos electrónicos de los empleados;
* las ciudades donde residen los clientes.

Recuperar únicamente las columnas necesarias recibe el nombre de ​**proyección**​, un concepto heredado directamente del Álgebra Relacional estudiada en las primeras clases del curso.

---

## ¿Qué es la proyección?

La proyección consiste en seleccionar únicamente determinadas columnas de una relación.

Visualmente:

```text
Tabla Cliente

+----+---------+------------+------------+---------+
| Id | Nombre  | Correo     | Ciudad     | Activo |
+----+---------+------------+------------+---------+

            │

            ▼

SELECT Nombre, Ciudad

            │

            ▼

+---------+------------+
| Nombre  | Ciudad     |
+---------+------------+
| Ana     | Santander  |
| Luis    | Bilbao     |
| Marta   | Oviedo     |
+---------+------------+
```

Las filas permanecen iguales.

Lo único que cambia es el conjunto de columnas mostrado.

---

## Seleccionar una única columna

La consulta más sencilla consiste en recuperar una sola columna.

```sql
SELECT Nombre
FROM Cliente;
```

Resultado:

| Nombre         |
| ---------------- |
| Ana Ruiz       |
| Luis Gómez    |
| Javier Torres  |
| Elena Sánchez |

Este tipo de consulta es muy habitual cuando únicamente necesitamos mostrar un listado de nombres.

---

## Seleccionar varias columnas

También podemos indicar varias columnas separadas por comas.

```sql
SELECT
    Nombre,
    Ciudad
FROM Cliente;
```

Resultado:

| Nombre         | Ciudad    |
| ---------------- | ----------- |
| Ana Ruiz       | Santander |
| Luis Gómez    | Bilbao    |
| Javier Torres  | Burgos    |
| Elena Sánchez | León     |

El orden de las columnas será exactamente el mismo en que aparecen escritas en la consulta.

---

## Cambiando el orden de las columnas

Las columnas no tienen por qué aparecer en el mismo orden que fueron definidas en la tabla.

Por ejemplo:

```sql
SELECT
    Ciudad,
    Nombre
FROM Cliente;
```

Resultado:

| Ciudad    | Nombre        |
| ----------- | --------------- |
| Santander | Ana Ruiz      |
| Bilbao    | Luis Gómez   |
| Burgos    | Javier Torres |

El orden del resultado depende completamente de la sentencia `SELECT`.

---

## Consultando otras tablas

Podemos aplicar exactamente la misma técnica sobre cualquier tabla.

Productos:

```sql
SELECT
    Nombre,
    Precio
FROM Producto;
```

Empleados:

```sql
SELECT
    Nombre,
    Cargo
FROM Empleado;
```

Categorías:

```sql
SELECT
    Nombre,
    Descripcion
FROM Categoria;
```

La sintaxis es siempre la misma.

---

## ¿Por qué evitar SELECT \*?

Aunque `SELECT *` resulta cómodo, en entornos profesionales suele evitarse por varias razones.

### 1. Mejor rendimiento

Si una tabla contiene veinte columnas y únicamente necesitamos dos, recuperar las veinte supone transmitir mucha más información de la necesaria.

Cuantas menos columnas se recuperen, menor será el volumen de datos enviado entre el servidor y la aplicación.

---

### 2. Mayor claridad

Observemos ambas consultas.

```sql
SELECT *
FROM Producto;
```

Frente a:

```sql
SELECT
    Nombre,
    Precio,
    Stock
FROM Producto;
```

La segunda consulta permite comprender inmediatamente qué información necesita el programa.

---

### 3. Mayor estabilidad

Si en el futuro se añade una nueva columna a la tabla, una consulta con `SELECT *` cambiará automáticamente su resultado.

En cambio, una consulta que especifica explícitamente las columnas continuará funcionando exactamente igual.

Por este motivo, en proyectos profesionales suele recomendarse escribir siempre las columnas necesarias.

---

## Relación con el Álgebra Relacional

En las primeras clases estudiamos el operador de proyección.

Su notación era:

```text
π Nombre, Ciudad (Cliente)
```

Su equivalente en SQL es:

```sql
SELECT
    Nombre,
    Ciudad
FROM Cliente;
```

Esta equivalencia demuestra nuevamente cómo SQL está basado directamente en los conceptos del Álgebra Relacional.

---

## Errores frecuentes

Los errores más habituales son:

* escribir mal el nombre de una columna;
* olvidar separar las columnas mediante comas;
* intentar consultar una columna que no existe;
* abusar de `SELECT *` cuando solo son necesarias unas pocas columnas.

La mejor práctica consiste en seleccionar únicamente la información que realmente necesita la consulta.

---

## Ideas clave

* La proyección consiste en seleccionar determinadas columnas de una tabla.
* `SELECT *` devuelve todas las columnas.
* Es posible consultar una o varias columnas.
* El orden de las columnas depende del orden escrito en `SELECT`.
* En aplicaciones profesionales se recomienda evitar `SELECT *` siempre que sea posible.

