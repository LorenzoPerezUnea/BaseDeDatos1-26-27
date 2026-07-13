# Carga inicial de datos

## Introducción

Una vez creada la estructura de una base de datos, el siguiente paso consiste en poblarla con información.

En proyectos reales este proceso recibe el nombre de **carga inicial de datos** o ​**data seeding**​.

Gracias a él disponemos de una base de datos lista para comenzar a trabajar, realizar pruebas o desarrollar nuevas funcionalidades.

Durante el resto de la asignatura utilizaremos siempre un conjunto común de datos que irá creciendo conforme avancemos en el curso.

De este modo, todas las consultas, ejercicios y prácticas se realizarán sobre un escenario realista y coherente.

---

## ¿Por qué cargar datos iniciales?

Trabajar con tablas vacías resulta poco útil.

Sin información almacenada no podemos:

* realizar consultas;
* calcular estadísticas;
* practicar `JOIN`;
* utilizar funciones de agregación;
* comprobar restricciones.

Por ello, antes de comenzar el bloque dedicado a consultas SQL, construiremos un pequeño conjunto de datos representativo.

---

## Orden correcto de inserción

Cuando existen claves foráneas no podemos insertar la información en cualquier orden.

Debemos comenzar siempre por las tablas que no dependen de ninguna otra.

En nuestro caso práctico seguiremos el siguiente orden.

```text
Categoria

↓

Cliente

↓

Empleado

↓

Producto

↓

Pedido

↓

DetallePedido
```

De esta forma todas las claves foráneas encontrarán previamente los registros que necesitan referenciar.

---

## Ejemplo

Comenzaremos insertando algunas categorías.

```sql
INSERT INTO Categoria
(
    Nombre,
    Descripcion
)
VALUES
(
    'Portátiles',
    'Equipos portátiles'
),
(
    'Monitores',
    'Pantallas profesionales'
),
(
    'Periféricos',
    'Accesorios informáticos'
);
```

Posteriormente podremos insertar productos indicando la categoría correspondiente.

---

## Verificando la carga

Después de poblar una tabla conviene comprobar el número de registros.

Por ejemplo:

```sql
SELECT *
FROM Categoria;
```

Más adelante aprenderemos a utilizar funciones como `COUNT(*)` para realizar estas comprobaciones de forma mucho más eficiente.

---

## Scripts de inicialización

En proyectos profesionales es habitual almacenar todas las inserciones iniciales en uno o varios archivos SQL.

Por ejemplo:

```text
schema.sql

datos_iniciales.sql

datos_pruebas.sql
```

Esto permite reconstruir rápidamente una base de datos completa en cualquier ordenador o servidor.

Durante esta asignatura seguiremos una estrategia similar y construiremos progresivamente nuestro propio conjunto de datos reutilizable.

---

## Buenas prácticas

Al preparar datos iniciales conviene seguir algunas recomendaciones:

* utilizar información coherente;
* respetar las restricciones definidas;
* mantener siempre el mismo orden de inserción;
* comprobar el resultado después de cada bloque;
* documentar claramente el propósito de cada conjunto de datos.

Estas prácticas facilitarán enormemente las futuras sesiones del curso.

---

## Errores frecuentes

Uno de los errores más habituales consiste en insertar registros en tablas hijas antes de haber creado los registros correspondientes en las tablas padre.

También es frecuente mezclar datos inconsistentes o duplicados, dificultando posteriormente la realización de consultas y ejercicios.

### Ideas clave

* La carga inicial permite comenzar a trabajar con una base de datos completamente funcional.
* El orden de inserción depende de las relaciones entre tablas.
* Los datos iniciales deben ser coherentes y reutilizables.
* En proyectos reales suelen almacenarse en scripts SQL independientes.
* Nuestro caso práctico utilizará un conjunto común de datos durante el resto de la asignatura.

