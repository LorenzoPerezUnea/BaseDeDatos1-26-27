# Índices desde el diseño

Cuando pensamos en una base de datos solemos centrarnos en almacenar información correctamente.

Sin embargo, también debemos preocuparnos por ​**cómo se recuperará esa información**​.

Aquí aparecen los ​**índices**​.

Aunque los índices se crean físicamente durante la implementación, es recomendable planificarlos ya en la fase de diseño lógico.

### ¿Qué es un índice?

Un índice es una estructura auxiliar que permite localizar registros mucho más rápidamente.

Su funcionamiento puede compararse con el índice de un libro.

Si queremos buscar un tema concreto, no leemos todas las páginas.

Consultamos el índice y accedemos directamente al apartado deseado.

Las bases de datos funcionan de manera muy similar.

### ¿Por qué planificarlos desde el diseño?

Durante el análisis del negocio ya conocemos cuáles serán las consultas más habituales.

Por ejemplo:

* buscar un cliente por su identificador;
* localizar un pedido concreto;
* obtener todos los pedidos de un cliente;
* buscar productos por categoría.

Estas operaciones nos permiten anticipar qué columnas necesitarán índices.

### Índices automáticos

En la mayoría de los SGBD, incluyendo MySQL, la clave primaria genera automáticamente un índice.

Por ejemplo:

```text
CLIENTE

IdCliente
```

No será necesario crear otro índice adicional sobre esa misma columna.

### Índices recomendables

En nuestro caso práctico resultará razonable indexar columnas como:

```text
PEDIDO

IdCliente
```

porque muchas consultas recuperarán los pedidos de un cliente.

También será útil indexar:

```text
PRODUCTO

IdCategoria
```

para localizar rápidamente todos los productos pertenecientes a una categoría.

### ¿Conviene indexar todas las columnas?

No.

Cada índice ocupa espacio adicional y debe actualizarse cuando cambian los datos.

Crear índices innecesarios puede incluso reducir el rendimiento de las operaciones de inserción y actualización.

Por ello, solo deben indexarse aquellas columnas que realmente participarán con frecuencia en búsquedas, filtros, ordenaciones o relaciones.

### Una regla sencilla

Como norma general, conviene plantearse índices sobre:

* claves primarias;
* claves foráneas;
* columnas utilizadas habitualmente en búsquedas;
* columnas utilizadas para ordenar resultados.

El resto deberá evaluarse según las necesidades reales del sistema.

### Ideas clave

* Los índices aceleran las consultas.
* Deben planificarse durante el diseño lógico.
* Las claves primarias suelen generar índices automáticamente.
* No todas las columnas necesitan un índice.
* Un exceso de índices también puede perjudicar el rendimiento.

