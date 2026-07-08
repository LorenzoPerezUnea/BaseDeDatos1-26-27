# Documentación del modelo

Diseñar correctamente una base de datos no es suficiente.

También es necesario documentarla.

Una base de datos profesional puede permanecer en funcionamiento durante muchos años y ser mantenida por distintos equipos de desarrollo.

Sin documentación, comprender el diseño original resulta cada vez más difícil.

### ¿Qué debe documentarse?

La documentación debe explicar tanto la estructura como el significado del modelo.

Entre los elementos más importantes se encuentran:

* finalidad de cada tabla;
* descripción de cada columna;
* claves primarias;
* claves foráneas;
* reglas de negocio;
* restricciones especiales.

El objetivo es que cualquier desarrollador pueda comprender el modelo sin necesidad de consultar al diseñador original.

### Un ejemplo

Una documentación sencilla para la tabla CLIENTE podría ser la siguiente.

| Elemento       | Descripción                              |
| ---------------- | ------------------------------------------- |
| Tabla          | CLIENTE                                   |
| Finalidad      | Almacena la información de los clientes. |
| Clave primaria | IdCliente                                 |
| Relaciones     | Un cliente puede realizar muchos pedidos. |
| Observaciones  | El correo electrónico debe ser único.   |

Este tipo de documentación resulta muy útil incluso en proyectos pequeños.

### Diagramas

Además del texto, es recomendable conservar el diagrama del modelo.

El diagrama proporciona una visión global difícil de obtener únicamente leyendo tablas.

Nuestro repositorio incluirá siempre:

* el diagrama Entidad-Relación;
* el modelo relacional;
* la documentación de las tablas.

### Diccionario de datos

Otra herramienta muy utilizada es el ​**diccionario de datos**​.

Se trata de un documento que describe cada columna de la base de datos.

Por ejemplo:

| Columna           | Significado                       |
| ------------------- | ----------------------------------- |
| IdCliente         | Identificador único del cliente. |
| Nombre            | Nombre completo del cliente.      |
| FechaRegistro     | Fecha de alta en el sistema.      |
| CorreoElectronico | Dirección principal de contacto. |

Cuando las bases de datos contienen cientos de columnas, este documento resulta imprescindible.

### Beneficios

Una buena documentación:

* facilita el mantenimiento;
* acelera la incorporación de nuevos desarrolladores;
* reduce errores;
* mejora la comunicación entre equipos.

Documentar no es una tarea secundaria.

Forma parte del propio diseño.

### Ideas clave

* Toda base de datos profesional debe documentarse.
* La documentación explica el significado del modelo.
* Los diagramas complementan la descripción textual.
* El diccionario de datos facilita la comprensión de las columnas.
* Una buena documentación prolonga la vida útil del sistema.

