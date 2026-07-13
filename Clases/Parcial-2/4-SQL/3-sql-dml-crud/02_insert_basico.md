# INSERT básico

## Introducción

La primera operación que aprenderemos dentro del Lenguaje de Manipulación de Datos será `INSERT`.

Después de haber dedicado varias clases a construir la estructura de nuestra base de datos, ha llegado el momento de comenzar a almacenar información real.

Cada cliente registrado, cada producto creado, cada empleado incorporado y cada pedido realizado comenzarán su existencia mediante una sentencia `INSERT`.

Es, probablemente, la instrucción DML más utilizada durante la fase inicial de cualquier proyecto.

Sin embargo, aunque su sintaxis sea sencilla, es importante adquirir desde el principio una metodología correcta de trabajo.

---

## ¿Qué hace INSERT?

La sentencia `INSERT` crea una nueva fila dentro de una tabla.

Cada ejecución añade exactamente un nuevo registro, salvo que utilicemos la variante de inserción múltiple que estudiaremos en el siguiente apartado.

Visualmente ocurre algo parecido a esto.

```text
Tabla Cliente

Antes

+-----------+---------+
| IdCliente | Nombre  |
+-----------+---------+
| 1         | Ana     |
| 2         | Luis    |
+-----------+---------+

↓

INSERT

↓

+-----------+---------+
| IdCliente | Nombre  |
+-----------+---------+
| 1         | Ana     |
| 2         | Luis    |
| 3         | Marta   |
+-----------+---------+
```

La estructura de la tabla no cambia.

Únicamente aumenta el número de registros almacenados.

---

## Sintaxis recomendada

Aunque SQL permite varias formas de escribir un `INSERT`, durante este curso utilizaremos siempre la siguiente.

```sql
INSERT INTO NombreTabla
(
    Columna1,
    Columna2,
    Columna3
)
VALUES
(
    Valor1,
    Valor2,
    Valor3
);
```

Observemos que:

* se especifican explícitamente las columnas;
* los valores aparecen en el mismo orden;
* el código resulta mucho más legible.

Esta será la convención utilizada durante todo el curso.

---

## Primer ejemplo

Insertemos nuestro primer cliente.

```sql
INSERT INTO Cliente
(
    Nombre,
    CorreoElectronico,
    Ciudad,
    FechaRegistro,
    Activo
)
VALUES
(
    'Ana Ruiz',
    'ana@empresa.com',
    'Santander',
    '2026-10-01',
    TRUE
);
```

No indicamos el valor de `IdCliente`.

¿Por qué?

Porque la columna está definida mediante `AUTO_INCREMENT`.

MySQL generará automáticamente el siguiente identificador disponible.

---

## Comprobando el resultado

Siempre que ejecutemos un `INSERT` debemos verificar inmediatamente el resultado.

Utilizaremos la siguiente consulta.

```sql
SELECT *
FROM Cliente;
```

Obtendremos una salida similar.

| IdCliente | Nombre   | CorreoElectronico                      | Ciudad    |
| ----------: | ---------- | ---------------------------------------- | ----------- |
|         1 | Ana Ruiz | [ana@empresa.com](mailto:ana@empresa.com) | Santander |

Aunque todavía no hemos estudiado formalmente `SELECT`, utilizaremos esta instrucción como herramienta de comprobación durante las prácticas.

Más adelante analizaremos todas sus posibilidades con detalle.

---

## Insertando solo algunas columnas

No es obligatorio proporcionar valores para todas las columnas.

Podemos omitir aquellas que:

* permitan `NULL`;
* tengan un valor `DEFAULT`;
* sean `AUTO_INCREMENT`.

Por ejemplo:

```sql
INSERT INTO Categoria
(
    Nombre
)
VALUES
(
    'Portátiles'
);
```

En este caso:

* `IdCategoria` será generado automáticamente;
* `Descripcion` tomará el valor `NULL`.

---

## Valores y tipos de datos

Cada valor debe ser compatible con el tipo de dato definido para la columna correspondiente.

Por ejemplo:

```sql
INSERT INTO Producto
(
    Nombre,
    Precio,
    Stock,
    Activo
)
VALUES
(
    'Ultrabook X15',
    1299.95,
    25,
    TRUE
);
```

Aquí observamos distintos tipos de datos trabajando conjuntamente:

* texto (`VARCHAR`);
* números decimales (`DECIMAL`);
* enteros (`INT`);
* valores booleanos (`BOOLEAN`).

MySQL comprobará automáticamente que cada valor sea compatible con la definición de la tabla.

---

## Casos reales

En una aplicación empresarial moderna, cada formulario de alta termina convirtiéndose en una sentencia `INSERT`.

Por ejemplo:

* registrar un cliente;
* crear un producto;
* dar de alta un proveedor;
* registrar un empleado;
* abrir una nueva incidencia.

Aunque el usuario únicamente pulse un botón, el servidor terminará ejecutando una o varias instrucciones SQL muy similares a las que estamos aprendiendo.

---

## Errores frecuentes

Uno de los errores más comunes consiste en omitir la lista de columnas.

Aunque MySQL lo permite, esta práctica hace que el código sea mucho más frágil frente a futuras modificaciones de la tabla.

También es frecuente escribir los valores en un orden diferente al de las columnas, produciendo errores de tipo o información almacenada en columnas incorrectas.

Finalmente, muchos estudiantes olvidan comprobar el resultado utilizando `SELECT`.

## Ideas clave

* `INSERT` añade nuevos registros a una tabla.
* Es recomendable indicar siempre la lista de columnas.
* `AUTO_INCREMENT` genera automáticamente los identificadores.
* Las columnas con `DEFAULT` o que admiten `NULL` pueden omitirse.
* Después de cada inserción conviene verificar el resultado mediante una consulta.

