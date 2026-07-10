# Primer esquema del caso práctico

## Introducción

Hasta este momento hemos aprendido a crear una base de datos, definir tablas, seleccionar tipos de datos y utilizar restricciones como `PRIMARY KEY`, `NOT NULL`, `DEFAULT` y `AUTO_INCREMENT`.

Sin embargo, todos los ejemplos realizados hasta ahora han utilizado una única tabla.

Ha llegado el momento de comenzar a construir la base de datos de la empresa comercial que nos acompañará durante el resto del curso.

Es importante recordar que ​**no pretendemos crear el modelo completo en una sola clase**​. Una base de datos profesional evoluciona gradualmente, incorporando nuevas entidades y relaciones conforme aparecen nuevos requisitos.

Nuestro objetivo en esta sesión será construir el primer esquema físico del sistema, formado por las entidades principales sobre las que trabajaremos durante las próximas semanas.

En este primer diseño ​**todavía no definiremos claves foráneas**​. Aunque las tablas estarán relacionadas conceptualmente, esperaremos a las próximas clases para estudiar formalmente la integridad referencial.

---

### El primer conjunto de entidades

Recordemos el caso práctico.

Nuestra empresa vende productos tecnológicos tanto en tiendas físicas como a través de Internet.

Inicialmente trabajaremos con cuatro entidades principales:

* Clientes.
* Empleados.
* Categorías.
* Productos.

Estas entidades constituyen el núcleo del negocio y servirán como base para incorporar posteriormente pedidos, facturas, inventario, proveedores y el resto del modelo.

---

### Creando el esquema inicial

A continuación ejecutaremos un único script que creará las cuatro primeras tablas.

```sql
USE empresa_tecnologica;

DROP TABLE IF EXISTS Producto;
DROP TABLE IF EXISTS Categoria;
DROP TABLE IF EXISTS Empleado;
DROP TABLE IF EXISTS Cliente;

CREATE TABLE Cliente (

    IdCliente INT AUTO_INCREMENT PRIMARY KEY,

    Nombre VARCHAR(100) NOT NULL,

    CorreoElectronico VARCHAR(150) NOT NULL,

    Ciudad VARCHAR(80),

    FechaRegistro DATE,

    Activo BOOLEAN DEFAULT TRUE

);

CREATE TABLE Empleado (

    IdEmpleado INT AUTO_INCREMENT PRIMARY KEY,

    Nombre VARCHAR(100) NOT NULL,

    Cargo VARCHAR(80),

    FechaContratacion DATE,

    Activo BOOLEAN DEFAULT TRUE

);

CREATE TABLE Categoria (

    IdCategoria INT AUTO_INCREMENT PRIMARY KEY,

    Nombre VARCHAR(80) NOT NULL,

    Descripcion VARCHAR(250)

);

CREATE TABLE Producto (

    IdProducto INT AUTO_INCREMENT PRIMARY KEY,

    Nombre VARCHAR(120) NOT NULL,

    Precio DECIMAL(10,2) NOT NULL,

    Stock INT DEFAULT 0,

    Activo BOOLEAN DEFAULT TRUE

);
```

Aunque todavía no existan relaciones entre ellas, ya disponemos de la estructura básica sobre la que construiremos el resto del sistema.

---

### Comprobando el resultado

Después de ejecutar el script, comprobaremos que todas las tablas han sido creadas correctamente.

```sql
SHOW TABLES;
```

La salida debería mostrar:

| Tables\_in\_empresa\_tecnologica |
| ---------------------------------- |
| Categoria                        |
| Cliente                          |
| Empleado                         |
| Producto                         |

A continuación inspeccionaremos la estructura de cada tabla.

```sql
DESC Cliente;

DESC Empleado;

DESC Categoria;

DESC Producto;
```

Acostumbrarse a verificar la estructura después de cada modificación es una excelente práctica profesional.

---

### ¿Por qué todavía no aparecen relaciones?

Muchos estudiantes se sorprenden al comprobar que la tabla `Producto` no contiene ninguna referencia a `Categoria`.

La razón es puramente didáctica.

Hasta este momento únicamente hemos estudiado la creación de tablas y las restricciones aplicables a columnas individuales.

Las relaciones entre tablas introducen nuevos conceptos como:

* claves foráneas;
* integridad referencial;
* actualización en cascada;
* eliminación restringida.

Estos temas merecen un estudio específico y aparecerán en las próximas clases.

Construir primero las entidades y después conectarlas permite comprender mucho mejor el funcionamiento del modelo relacional.

---

### Evolución del modelo

El esquema que acabamos de crear representa únicamente el punto de partida.

En las próximas semanas iremos ampliándolo.

```text
Cliente
Empleado
Categoria
Producto
        │
        ▼
Pedidos
LíneasPedido
Facturas
Pagos
Inventario
Proveedores
Compras
Envíos
Devoluciones
...
```

Esta evolución progresiva reproducirá el crecimiento natural de un proyecto real.

---

### Casos reales

En proyectos profesionales rara vez se implementa toda la base de datos en un único día.

Normalmente el modelo evoluciona por iteraciones.

Cada nueva versión incorpora entidades adicionales, nuevas restricciones y mejoras derivadas de las necesidades del negocio.

Nuestro caso práctico seguirá exactamente esa misma filosofía.

---

### Errores frecuentes

Un error habitual consiste en intentar crear todas las tablas del sistema antes de haber comprendido los conceptos básicos del lenguaje DDL.

También es frecuente comenzar a definir claves foráneas sin haber diseñado previamente las entidades principales.

Construir primero un esquema sencillo facilita enormemente la comprensión del resto del curso.

### Ideas clave

* El caso práctico comienza a materializarse como una base de datos real.
* Las primeras entidades del sistema son Cliente, Empleado, Categoría y Producto.
* El modelo crecerá progresivamente durante todo el semestre.
* Las relaciones entre tablas se incorporarán en próximas clases.
* Trabajar de forma incremental es una práctica habitual en proyectos profesionales.

