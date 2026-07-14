# Cómo trabaja MySQL

## Introducción

Cuando escribimos una consulta SQL solemos pensar que MySQL la ejecuta exactamente en el orden en que aparece escrita.

Por ejemplo:

```sql
SELECT Nombre, Apellidos
FROM Cliente
WHERE Ciudad = 'Madrid'
ORDER BY Apellidos;
```

Sin embargo, internamente el proceso es mucho más complejo.

Antes de acceder a un solo registro, MySQL analiza la consulta, estudia la estructura de la base de datos, evalúa los índices disponibles y calcula diferentes estrategias de ejecución.

El componente encargado de realizar este trabajo recibe el nombre de **optimizador de consultas** (*Query Optimizer*).

Comprender cómo trabaja este componente es fundamental para entender posteriormente por qué una consulta rápida puede convertirse en una consulta muy lenta simplemente cambiando una condición o eliminando un índice.

## El recorrido de una consulta

Desde que una consulta llega al servidor hasta que el usuario recibe el resultado, MySQL realiza varias etapas internas.

De forma simplificada, el proceso puede representarse así:

```text
Consulta SQL

↓

Análisis léxico

↓

Análisis sintáctico

↓

Comprobación semántica

↓

Optimizador

↓

Plan de ejecución

↓

Motor de almacenamiento

↓

Resultado
```

Aunque el usuario únicamente observa el resultado final, cada una de estas fases influye en el rendimiento.

## Paso 1. Recepción de la consulta

Todo comienza cuando el cliente envía una sentencia SQL.

```sql
SELECT *
FROM Producto
WHERE Categoria = 'Portátiles';
```

El servidor recibe la consulta como una cadena de texto.

En este momento todavía no sabe si la consulta es correcta ni cómo debe ejecutarla.

## Paso 2. Análisis léxico

En esta fase MySQL divide la consulta en pequeñas unidades llamadas **tokens**.

Por ejemplo:

```sql
SELECT
```

es una palabra reservada.

```sql
Producto
```

es un identificador.

```sql
WHERE
```

es otra palabra reservada.

```sql
'Portátiles'
```

es un valor literal.

Este proceso es similar al que realiza un compilador al analizar un programa.

## Paso 3. Análisis sintáctico

Una vez identificados los tokens, MySQL comprueba que la estructura de la consulta sea válida.

Por ejemplo:

```sql
SELECT
FROM Producto;
```

producirá un error porque falta la lista de columnas.

En cambio:

```sql
SELECT *
FROM Producto;
```

supera correctamente esta fase.

## Paso 4. Comprobación semántica

Ahora el servidor verifica que todos los elementos utilizados existan realmente.

Por ejemplo:

```sql
SELECT Precio
FROM Producto;
```

Si la columna `Precio` existe, la consulta continúa.

Si escribimos:

```sql
SELECT PrecioVenta
FROM Producto;
```

y esa columna no existe, MySQL devolverá un error antes de intentar ejecutar la consulta.

También comprueba aspectos como:

- Existencia de tablas.
- Existencia de vistas.
- Permisos del usuario.
- Tipos de datos.
- Compatibilidad entre expresiones.

## Paso 5. El optimizador

Una vez comprobada la validez de la consulta comienza la fase más interesante.

El optimizador intenta responder a una pregunta:

> ¿Cuál es la forma más rápida de obtener el resultado solicitado?

Para ello estudia diferentes posibilidades.

Por ejemplo:

- ¿Conviene utilizar un índice?
- ¿Es mejor recorrer la tabla completa?
- ¿Qué tabla debe leerse primero en un JOIN?
- ¿Qué algoritmo resulta más eficiente?
- ¿Puede reutilizar algún índice existente?

Cada alternativa recibe una estimación de coste.

Finalmente selecciona aquella que considera más eficiente.

## Un ejemplo

Supongamos esta consulta.

```sql
SELECT *
FROM Cliente
WHERE IdCliente = 5000;
```

Si `IdCliente` es la clave primaria, el optimizador probablemente elegirá un acceso mediante índice.

En cambio:

```sql
SELECT *
FROM Cliente
WHERE Observaciones LIKE '%urgente%';
```

Es posible que determine que utilizar un índice no aporta ninguna ventaja y prefiera recorrer toda la tabla.

## Paso 6. Generación del plan de ejecución

Después de elegir la mejor estrategia, MySQL construye un **plan de ejecución**.

Este plan describe exactamente cómo se obtendrán los datos.

Entre otras decisiones indica:

- Qué índice utilizar.
- Qué tablas leer primero.
- Cómo resolver los JOIN.
- Qué filtros aplicar.
- Cuándo ordenar los resultados.

La herramienta `EXPLAIN`, que estudiaremos más adelante, permite visualizar este plan.

## Paso 7. Acceso al motor de almacenamiento

Una vez definido el plan, MySQL solicita los datos al motor de almacenamiento correspondiente.

En nuestro curso trabajamos con **InnoDB**.

Este motor es el encargado de:

- Leer páginas del disco.
- Gestionar índices.
- Controlar bloqueos.
- Administrar transacciones.
- Mantener los registros en memoria cuando es posible.

El optimizador decide **qué hacer**.

El motor decide **cómo acceder físicamente a los datos**.

## Paso 8. Devolver el resultado

Finalmente MySQL envía los registros obtenidos al cliente.

En ocasiones el resultado necesita operaciones adicionales antes de ser devuelto.

Por ejemplo:

- Ordenación (`ORDER BY`).
- Agrupación (`GROUP BY`).
- Eliminación de duplicados (`DISTINCT`).
- Funciones de agregación.

Solo cuando todas estas tareas han finalizado, el usuario recibe la respuesta.

## ¿Siempre elige el mejor plan?

El objetivo del optimizador es seleccionar el plan más eficiente.

Sin embargo, trabaja con estimaciones.

Estas estimaciones se basan en estadísticas sobre las tablas y los índices.

Si dichas estadísticas no reflejan correctamente la distribución real de los datos, el optimizador puede tomar decisiones poco acertadas.

Por ello, una parte importante de la optimización consiste en comprender por qué MySQL ha elegido un determinado plan de ejecución.

## Analogía

Imaginemos un repartidor que debe entregar paquetes en una ciudad.

Antes de salir no comienza a conducir inmediatamente.

Primero calcula la mejor ruta.

Tiene varias alternativas.

Puede utilizar autopistas, carreteras secundarias o calles urbanas.

Elige aquella que considera más rápida.

El optimizador actúa exactamente igual.

No ejecuta la consulta de inmediato.

Primero busca el camino más eficiente.

## Buenas prácticas

- No asumir que MySQL ejecuta las consultas en el orden escrito.
- Confiar en el optimizador, pero verificar sus decisiones mediante `EXPLAIN`.
- Mantener actualizadas las estadísticas de la base de datos.
- Comprender que dos consultas equivalentes pueden generar planes completamente distintos.
- Analizar siempre las consultas críticas desde el punto de vista del plan de ejecución.

## Conclusiones

Antes de ejecutar una consulta, MySQL realiza un complejo proceso de análisis y optimización. El optimizador estudia diferentes estrategias, estima su coste y genera un plan de ejecución que posteriormente utilizará el motor de almacenamiento para recuperar la información. Comprender este proceso resulta esencial para interpretar correctamente el rendimiento de una consulta y optimizarla cuando sea necesario.

## Ideas clave

- MySQL no ejecuta directamente la consulta escrita por el usuario.
- El optimizador analiza distintas estrategias antes de acceder a los datos.
- El plan de ejecución describe cómo se obtendrá la información.
- El motor de almacenamiento ejecuta físicamente dicho plan.
- `EXPLAIN` permitirá visualizar estas decisiones en los siguientes apartados.

