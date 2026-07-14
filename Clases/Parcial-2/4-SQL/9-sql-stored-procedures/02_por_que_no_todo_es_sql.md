# ¿Por qué no todo es SQL?

## Introducción

SQL fue diseñado como un ​**lenguaje declarativo**​.

Esto significa que normalmente indicamos ​**qué queremos obtener**​, no ​**cómo debe conseguirse**​.

Por ejemplo:

```sql
SELECT *
FROM Cliente;
```

No indicamos cómo recorrer la tabla.

El motor de la base de datos decide la mejor forma de hacerlo.

Este enfoque funciona muy bien para consultar datos, pero presenta limitaciones cuando queremos implementar procesos más complejos.

---

## El problema

Supongamos que queremos registrar una venta.

Antes de insertar el pedido debemos comprobar:

* que el cliente existe;
* que el producto existe;
* que hay suficiente stock;
* que la cantidad solicitada es válida.

Después debemos:

* insertar el pedido;
* descontar el stock;
* registrar la operación.

Una única sentencia SQL no puede expresar fácilmente toda esa lógica.

Necesitamos algo más.

---

## La lógica de negocio

En programación solemos trabajar con estructuras como:

```text
Si ocurre A

↓

Hacer B

↓

En caso contrario

↓

Hacer C
```

O también:

```text
Mientras ocurra una condición

↓

Repetir una acción
```

Este tipo de comportamiento no forma parte del SQL clásico.

Para ello MySQL incorpora un lenguaje procedimental que permite construir algoritmos completos.

---

## Comparación

### SQL tradicional

```sql
SELECT *
FROM Producto
WHERE Stock > 0;
```

Consulta información.

---

### SQL procedimental

```text
SI existe el producto

↓

SI hay suficiente stock

↓

Insertar pedido

↓

Actualizar inventario

↓

Registrar operación
```

Ahora existe una secuencia de decisiones.

---

## Un ejemplo cotidiano

Imaginemos un cajero automático.

Una simple consulta SQL equivaldría a preguntar:

> ¿Cuál es el saldo de la cuenta?

Un procedimiento sería todo el proceso de retirar dinero:

1. Comprobar la tarjeta.
2. Verificar el PIN.
3. Comprobar el saldo.
4. Validar el importe solicitado.
5. Descontar el dinero.
6. Registrar la operación.
7. Imprimir el recibo.

No basta con una única consulta.

Se necesita una secuencia de instrucciones.

---

## ¿Por qué ejecutar lógica dentro de MySQL?

Existen varias razones.

* Reducir el código repetido en las aplicaciones.
* Ejecutar procesos cerca de los datos.
* Garantizar que todas las aplicaciones utilicen las mismas reglas.
* Disminuir el número de consultas enviadas al servidor.
* Mejorar la organización del sistema.

No obstante, también hay que evitar trasladar toda la lógica de una aplicación a la base de datos.

Lo habitual es repartir las responsabilidades entre la aplicación y el SGBD.

---

## Lo que aprenderemos

En los próximos apartados veremos cómo un procedimiento puede incluir:

* parámetros;
* variables;
* condiciones;
* bucles;
* manejo de errores;
* consultas SQL.

Con estas herramientas podremos construir pequeños programas que se ejecutan directamente dentro de MySQL.

---

## Ideas clave

* SQL clásico está orientado a describir consultas.
* Algunos procesos requieren lógica de programación.
* Los procedimientos almacenados permiten incorporar esa lógica al servidor.
* Constituyen una herramienta fundamental en aplicaciones profesionales.
* Combinan instrucciones SQL con estructuras propias de un lenguaje de programación.

