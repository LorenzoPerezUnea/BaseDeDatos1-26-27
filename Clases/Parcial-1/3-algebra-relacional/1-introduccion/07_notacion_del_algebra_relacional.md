# Notación del Álgebra Relacional

## Introducción

Hasta este momento hemos comprendido por qué nació el Álgebra Relacional, cuál es su relación con SQL y qué tipo de operaciones realiza sobre las relaciones.

Sin embargo, todavía no hemos visto cómo se escriben esas operaciones.

Al igual que las matemáticas utilizan símbolos para representar sumas, productos o funciones, el Álgebra Relacional posee una notación propia que permite expresar consultas de forma breve, precisa y completamente libre de ambigüedades.

A primera vista esta notación puede parecer extraña. Es habitual encontrar letras griegas, operadores poco familiares y expresiones que recuerdan más a un libro de matemáticas que a un lenguaje de programación.

No obstante, tras unos pocos ejemplos se descubre que su lógica es extraordinariamente sencilla y que, además, ayuda a comprender mucho mejor las consultas SQL.

En este capítulo conoceremos la notación básica que utilizaremos durante el resto del curso.

### Una notación para expresar operaciones

Recordemos que el Álgebra Relacional no pretende ser un lenguaje de programación.

Su objetivo consiste en describir operaciones sobre relaciones de forma rigurosa.

Para conseguirlo utiliza símbolos que representan acciones muy concretas.

Los más importantes son:

| Símbolo | Operación          | Significado general                                              |
| ---------- | --------------------- | ------------------------------------------------------------------ |
| σ       | Selección          | Filtrar tuplas                                                   |
| π       | Proyección         | Seleccionar atributos                                            |
| ∪       | Unión              | Combinar relaciones compatibles                                  |
| −       | Diferencia          | Obtener las tuplas que aparecen en una relación pero no en otra |
| ×       | Producto cartesiano | Combinar todas las tuplas posibles de dos relaciones             |
| ρ       | Renombrado          | Cambiar temporalmente el nombre de una relación o atributo      |

Cada uno de estos operadores tiene reglas muy precisas sobre cómo puede utilizarse.

A lo largo del curso los estudiaremos individualmente.

### La importancia de la precisión

Una de las ventajas de esta notación es que evita interpretaciones ambiguas.

Por ejemplo, la expresión:

```text
σ Ciudad = 'Santander' (Cliente)
```

debe leerse como:

> "Aplicar una selección sobre la relación Cliente conservando únicamente aquellas tuplas cuya ciudad sea Santander."

La estructura siempre es la misma.

Primero aparece el operador.

Después la condición, cuando exista.

Finalmente la relación sobre la que se aplica.

Una vez comprendido este patrón resulta muy sencillo interpretar expresiones mucho más complejas.

### Leyendo las expresiones de dentro hacia fuera

Muchos estudiantes intentan leer las expresiones algebraicas de izquierda a derecha, igual que leen una frase.

Sin embargo, esa estrategia suele generar confusión.

Es preferible interpretarlas siguiendo el orden en que realmente se ejecutan las operaciones.

Por ejemplo:

```text
π Nombre (
    σ Ciudad='Santander' (
        Cliente
    )
)
```

El proceso mental sería el siguiente:

1. Partimos de la relación ​**Cliente**​.
2. Filtramos únicamente los clientes cuya ciudad sea Santander.
3. Sobre el resultado anterior conservamos únicamente el atributo ​**Nombre**​.

La consulta completa puede leerse casi como una receta.

Cada operador transforma el resultado producido por el anterior.

### La composición de operadores

Una de las propiedades más elegantes del Álgebra Relacional consiste en que las operaciones pueden componerse unas con otras.

Esto significa que el resultado de un operador puede convertirse inmediatamente en la entrada del siguiente.

Por ejemplo:

```text
Cliente
    ↓
Selección
    ↓
Proyección
    ↓
Renombrado
    ↓
Resultado final
```

Esta capacidad de composición permite construir consultas muy complejas utilizando únicamente un pequeño conjunto de operadores básicos.

La idea recuerda al funcionamiento de una cadena de montaje, donde cada estación recibe el trabajo realizado por la anterior y produce un nuevo resultado que será procesado posteriormente.

### Nuestro caso de estudio

Supongamos que el departamento comercial desea conocer el nombre y el correo electrónico de todos los clientes registrados en Santander.

Desde el punto de vista del Álgebra Relacional podríamos describir el proceso así:

1. Comenzar con la relación ​**Cliente**​.
2. Seleccionar únicamente los clientes de Santander.
3. Proyectar únicamente los atributos Nombre y CorreoElectronico.

Aunque todavía no escribiremos la expresión completa utilizando todos los símbolos, ya podemos comprender perfectamente la secuencia lógica de operaciones.

Más adelante veremos que esta misma secuencia se traducirá de forma casi directa a una sentencia SQL.

### ¿Es necesario memorizar todos los símbolos?

No.

Durante las primeras semanas resulta mucho más importante comprender qué hace cada operador que memorizar su representación gráfica.

Con la práctica, los símbolos terminan resultando tan naturales como los operadores matemáticos tradicionales.

Del mismo modo que nadie necesita pensar qué significa el signo "+" después de años utilizándolo, la notación del Álgebra Relacional acaba convirtiéndose en una herramienta de trabajo habitual.

### Errores frecuentes

Uno de los errores más habituales consiste en intentar interpretar las expresiones como si fueran código SQL.

Aunque ambos lenguajes describen operaciones similares, su forma de escribirlas es completamente distinta.

También es frecuente olvidar que cada operador trabaja siempre sobre relaciones completas y no sobre filas individuales de manera aislada.

### Ideas clave

* El Álgebra Relacional utiliza una notación simbólica para describir operaciones sobre relaciones.
* Cada símbolo representa un operador perfectamente definido.
* Las expresiones se interpretan siguiendo la secuencia de operaciones que transforman una relación en otra.
* Los operadores pueden componerse para construir consultas cada vez más complejas.
* Comprender la notación facilitará enormemente la transición hacia SQL.

