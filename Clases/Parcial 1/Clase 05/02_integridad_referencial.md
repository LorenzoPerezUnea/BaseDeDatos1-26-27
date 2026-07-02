## Integridad referencial

La integridad referencial es una propiedad de los esquemas relacionales que garantiza la coherencia de las referencias entre relaciones cuando se utilizan claves foráneas.

En un esquema relacional, una clave foránea (foreign key) es un atributo o conjunto de atributos en una relación que apunta a la clave primaria de otra relación; la integridad referencial exige que cada valor presente en la clave foránea exista previamente como valor de la clave primaria de la relación referenciada, o bien que la clave foránea acepte valores nulos cuando la semántica del modelo lo permita.

Esta restricción evita referencias “colgantes” —es decir, tuplas que apuntan a identificadores inexistentes— y por tanto preserva la consistencia lógica de los datos a través de las diferentes relaciones del esquema.

Los sistemas de gestión de bases de datos implementan la integridad referencial mediante constraints declarativos que se comprueban en tiempo de modificación: al insertar o actualizar una tupla que contiene una clave foránea, el sistema verifica la existencia del valor correspondiente en la relación referenciada; al eliminar o modificar una tupla referenciada, debe definirse cómo se propaga el efecto a las tuplas que la referencian.

### Acciones

Las acciones de propagación habituales incluyen: RESTRICT (o NO ACTION), que impide la operación si existen referencias; CASCADE, que propaga la eliminación o modificación a las tuplas referenciantes; SET NULL, que sustituye la clave foránea por NULL; y SET DEFAULT, que asigna un valor por defecto.

La elección entre estas políticas depende de las reglas de negocio y del diseño conceptual: por ejemplo, si la existencia de la tupla referenciada es imprescindible, RESTRICT preservará la integridad a costa de reducir la flexibilidad; si la relación es puramente histórica o redundante, CASCADE puede simplificar la limpieza de datos.

Además de la verificación inmediata, algunos SGBD permiten definir constraints diferidos (deferred), que aplazan la comprobación de la integridad referencial hasta el final de una transacción.

Esto resulta útil cuando varias modificaciones interdependientes se realizan dentro de la misma transacción y, temporalmente, las referencias quedarían inválidas hasta que se complete el conjunto de cambios.

El empleo de constraints diferidos debe manejarse con cuidado, porque facilita operaciones complejas pero también puede ocultar errores lógicos si no se diseña correctamente la secuencia de actualizaciones.

Desde el punto de vista del diseño, la integridad referencial es una herramienta clave para modelar dependencias entre entidades: obliga a formalizar relaciones padre-hijo, a decidir la cardinalidad y la obligatoriedad de la relación, y a definir explícitamente la semántica de la eliminación y actualización en cascada.

A nivel de implementación, la existencia de claves foráneas y de las políticas de propagación condiciona estrategias de indexación y de optimización, ya que las operaciones de modificación deben comprobar y, en su caso, afectar a otras relaciones, con impacto en concurrencia y rendimiento.

Por tanto, al diseñar esquemas relacionales conviene documentar claramente las claves foráneas, sus dependencias y las acciones esperadas ante modificaciones, para que tanto la lógica de la aplicación como el propio SGBD mantengan la coherencia de los datos.

