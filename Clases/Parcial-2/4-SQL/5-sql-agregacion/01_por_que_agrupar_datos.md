# ¿Por qué agrupar datos?

## Introducción

Hasta este momento todas nuestras consultas devolvían listas de registros.

Por ejemplo:

* todos los clientes;
* todos los productos;
* todos los empleados.

Sin embargo, muchas veces esa información es excesiva.

Un director comercial no necesita visualizar miles de pedidos para saber cómo está funcionando la empresa.

Lo que realmente necesita son ​**indicadores**​.

Por ejemplo:

* número total de clientes;
* importe medio de los pedidos;
* producto más caro;
* ventas por categoría;
* número de empleados por departamento.

Estas preguntas no se responden mostrando registros individuales, sino ​**resumiendo la información**​.

---

## Del dato a la información

Observemos la diferencia.

Una consulta tradicional devuelve algo parecido a esto:

| Producto  | Precio |
| ----------- | -------: |
| Ratón    |     25 |
| Monitor   |    280 |
| SSD       |    120 |
| Portátil |    950 |

Esta información es útil, pero obliga al usuario a interpretar los datos manualmente.

En cambio, una consulta agregada puede devolver simplemente:

| Precio medio |
| -------------: |
|       343.75 |

Ahora la información ya está resumida y preparada para la toma de decisiones.

---

## El papel de las funciones de agregación

Las funciones de agregación permiten combinar múltiples registros para obtener un único resultado.

Por ejemplo:

* contar registros;
* sumar cantidades;
* calcular medias;
* localizar máximos;
* localizar mínimos.

Estas operaciones aparecen continuamente en informes empresariales.

---

## ¿Qué significa agrupar?

Agrupar consiste en dividir los registros en conjuntos que comparten alguna característica común.

Por ejemplo, podemos agrupar los productos por categoría.

```text
Categoría

Portátiles

    ├── Producto A
    ├── Producto B
    └── Producto C

Monitores

    ├── Producto D
    ├── Producto E

Periféricos

    ├── Producto F
    ├── Producto G
    ├── Producto H
```

Una vez creados los grupos podremos calcular estadísticas para cada uno de ellos.

---

## Ejemplos reales

En una empresa es habitual responder preguntas como:

* ¿Cuántos productos existen por categoría?
* ¿Cuál es el precio medio de cada categoría?
* ¿Qué ciudad tiene más clientes?
* ¿Cuántos empleados trabajan en cada departamento?
* ¿Cuál es el salario máximo por departamento?

Todas estas consultas utilizan agrupaciones.

---

## Agrupar no significa ordenar

Es importante no confundir ambos conceptos.

**ORDER BY**

Organiza los registros.

**GROUP BY**

Forma conjuntos de registros con características comunes.

Aunque ambas cláusulas suelen aparecer juntas, realizan funciones completamente diferentes.

---

## Relación con el Álgebra Relacional

En el Álgebra Relacional clásica no existía un operador específico de agrupación.

Las funciones de agregación fueron incorporadas posteriormente por SQL para responder a necesidades reales de análisis de información.

Por este motivo constituyen una de las ampliaciones más importantes que SQL aporta respecto al modelo relacional original.

---

## Ideas clave

* Agrupar permite resumir grandes cantidades de información.
* Las agrupaciones generan indicadores útiles para la toma de decisiones.
* Las funciones de agregación trabajan sobre grupos de registros.
* `GROUP BY` y `ORDER BY` son conceptos completamente diferentes.
* El análisis de datos comienza con la capacidad de resumir información de forma correcta.

