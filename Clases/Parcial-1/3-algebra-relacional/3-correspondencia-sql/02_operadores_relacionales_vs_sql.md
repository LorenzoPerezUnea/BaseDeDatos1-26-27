# Operadores relacionales vs SQL

## Introducción

Una vez comprendida la relación entre ambos lenguajes, resulta natural preguntarse cómo se corresponde cada operador del Álgebra Relacional con la sintaxis de SQL.

Aunque SQL incorpora muchas características adicionales, la mayoría de sus consultas básicas pueden explicarse mediante un pequeño conjunto de operadores relacionales.

Conocer estas equivalencias permitirá traducir consultas en ambos sentidos durante el resto de la clase.

### Desarrollo

La siguiente tabla resume las correspondencias fundamentales.

| Álgebra Relacional | SQL        | Función principal               |
| --------------------- | ------------ | ---------------------------------- |
| π                  | SELECT     | Elegir columnas                  |
| σ                  | WHERE      | Filtrar filas                    |
| ×                  | CROSS JOIN | Producto cartesiano              |
| ⋈                  | JOIN       | Combinar relaciones              |
| ∪                  | UNION      | Unión de resultados             |
| ∩                  | INTERSECT  | Intersección                    |
| −                  | EXCEPT     | Diferencia                       |
| ρ                  | AS         | Renombrar relaciones o atributos |

Es importante destacar que la equivalencia es conceptual y no estrictamente sintáctica.

Mientras que el Álgebra Relacional representa una secuencia de operaciones matemáticas, SQL adopta un estilo declarativo en el que el usuario describe el resultado que desea obtener.

### Ejemplos

| Álgebra Relacional         | SQL                                                |
| ----------------------------- | ---------------------------------------------------- |
| π Nombre (Cliente)         | `SELECT Nombre FROM Cliente;`                  |
| σ Ciudad='Bilbao'(Cliente) | `SELECT * FROM Cliente WHERE Ciudad='Bilbao';` |
| Cliente ⋈ Pedido           | `FROM Cliente JOIN Pedido ...`                 |

A lo largo de esta clase cada una de estas equivalencias se estudiará con mayor profundidad.

### Errores frecuentes

Un error habitual consiste en asumir que cada palabra reservada de SQL tiene un operador equivalente en el Álgebra Relacional.

Esto no siempre es cierto.

SQL incorpora funcionalidades como ordenación, agregación, funciones analíticas o modificación de datos que no forman parte del Álgebra Relacional clásica.

Por ello, la correspondencia debe entenderse como una relación entre los conceptos fundamentales y no como una traducción literal de todo el lenguaje.

### Ideas clave

* La mayoría de las consultas SQL básicas pueden expresarse mediante Álgebra Relacional.
* Cada operador relacional posee una cláusula SQL equivalente o muy similar.
* SQL añade numerosas funcionalidades que van más allá del Álgebra Relacional clásica.
* Comprender estas equivalencias facilita la traducción entre ambos lenguajes.
* La correspondencia es conceptual y constituye la base del funcionamiento interno de los SGBD.
  

