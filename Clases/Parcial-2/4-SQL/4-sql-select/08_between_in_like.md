# BETWEEN, IN y LIKE

## Introducción

Hasta ahora hemos aprendido a filtrar registros mediante operadores relacionales (`=`, `>`, `<`, `>=`, `<=`, `<>`) y operadores lógicos (`AND`, `OR`, `NOT`).

Sin embargo, existen situaciones muy habituales en las que estas herramientas resultan poco cómodas.

Por ejemplo:

* buscar productos cuyo precio esté entre 100 y 500 euros;
* obtener clientes que pertenezcan a varias ciudades concretas;
* localizar personas cuyo nombre empiece por una determinada letra;
* buscar direcciones de correo pertenecientes a un dominio específico.

Para resolver estos problemas SQL incorpora varios operadores especializados que simplifican enormemente las consultas.

Los más utilizados son:

* `BETWEEN`
* `IN`
* `LIKE`

Aunque internamente muchas de estas consultas podrían escribirse utilizando operadores relacionales, estas construcciones hacen el código mucho más legible.

---

## BETWEEN

`BETWEEN` permite comprobar si un valor se encuentra dentro de un intervalo.

Su sintaxis general es:

```sql
SELECT columnas
FROM Tabla
WHERE columna BETWEEN valor1 AND valor2;
```

Es equivalente a escribir:

```sql
columna >= valor1
AND
columna <= valor2
```

---

### Ejemplo con precios

```sql
SELECT
    Nombre,
    Precio
FROM Producto
WHERE Precio BETWEEN 100 AND 500;
```

Resultado:

| Nombre       | Precio |
| -------------- | -------: |
| Monitor 27"  | 289.90 |
| SSD NVMe 2TB | 199.00 |

Observa que ​**los extremos también están incluidos**​.

Es decir, un producto cuyo precio sea exactamente 100 o exactamente 500 aparecerá en el resultado.

---

### BETWEEN con fechas

También resulta muy útil para consultar intervalos temporales.

```sql
SELECT
    Nombre,
    FechaRegistro
FROM Cliente
WHERE FechaRegistro
BETWEEN '2026-01-01'
AND '2026-03-31';
```

Este tipo de consulta aparece constantemente en informes empresariales.

---

## IN

En muchas ocasiones necesitamos comparar un mismo campo con varios valores.

Una primera posibilidad sería escribir:

```sql
WHERE Ciudad = 'Santander'
OR Ciudad = 'Bilbao'
OR Ciudad = 'Oviedo'
```

Aunque funciona correctamente, la consulta resulta larga y difícil de mantener.

`IN` simplifica este tipo de comparaciones.

```sql
SELECT
    Nombre,
    Ciudad
FROM Cliente
WHERE Ciudad IN
(
    'Santander',
    'Bilbao',
    'Oviedo'
);
```

El resultado es exactamente el mismo, pero la consulta es mucho más clara.

---

### IN con valores numéricos

También puede utilizarse con identificadores.

```sql
SELECT *
FROM Producto
WHERE IdCategoria IN
(
    1,
    3,
    5
);
```

La consulta recuperará únicamente los productos pertenecientes a esas categorías.

---

## LIKE

Mientras que los operadores anteriores buscan coincidencias exactas, `LIKE` permite realizar búsquedas por patrones.

Es una de las herramientas más utilizadas en buscadores y formularios.

Para ello utiliza caracteres comodín.

| Símbolo | Significado                      |
| ---------- | ---------------------------------- |
| `%`  | Cualquier cantidad de caracteres |
| `_`  | Un único carácter              |

---

### Buscar nombres que comienzan por una letra

```sql
SELECT
    Nombre
FROM Cliente
WHERE Nombre LIKE 'A%';
```

Resultado:

| Nombre         |
| ---------------- |
| Ana Ruiz       |
| Alberto Gómez |

Todos los nombres comienzan por la letra A.

---

### Buscar nombres que terminan en una letra

```sql
SELECT
    Nombre
FROM Cliente
WHERE Nombre LIKE '%a';
```

Aparecerán todos los nombres cuyo último carácter sea la letra "a".

---

### Buscar una palabra dentro de un texto

```sql
SELECT
    Nombre
FROM Producto
WHERE Nombre LIKE '%SSD%';
```

Resultado:

| Nombre       |
| -------------- |
| SSD NVMe 1TB |
| SSD SATA 2TB |

La palabra puede aparecer al principio, en medio o al final.

---

### El comodín "\_"

El carácter `_` representa exactamente un carácter.

Por ejemplo:

```sql
SELECT *
FROM Cliente
WHERE Nombre LIKE 'A_a';
```

Coincidiría con nombres como:

* Ana
* Ada

pero no con:

* Alberto
* Alejandro

---

## Buenas prácticas

Cada operador tiene un propósito concreto.

Utiliza:

* `BETWEEN` para intervalos.
* `IN` para listas de valores.
* `LIKE` para búsquedas parciales de texto.

Elegir el operador adecuado hace que las consultas sean mucho más fáciles de leer y mantener.

---

## Ideas clave

* `BETWEEN` permite consultar intervalos de valores.
* `IN` simplifica múltiples comparaciones de igualdad.
* `LIKE` realiza búsquedas mediante patrones.
* `%` representa cualquier número de caracteres.
* `_` representa exactamente un carácter.
* Estos operadores aparecen constantemente en aplicaciones reales.

