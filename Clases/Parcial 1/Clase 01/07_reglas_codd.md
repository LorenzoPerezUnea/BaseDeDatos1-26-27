# Reglas de Codd

Propuestas por Edgar F. Codd para definir un **SGBD relacional**.
En total son 12 reglas; las más importantes:

# 📜 Las 12 Reglas de Codd (Resumen Continuo)

Codd definió 13 reglas (contando la regla 0) para determinar si un SGBD es verdaderamente relacional.
**Regla 0:** Todo sistema que se diga relacional debe gestionar bases de datos usando exclusivamente sus capacidades relacionales. Ejemplo: poder crear, modificar y consultar todo mediante SQL sin editar archivos a mano.

**1. Regla de Información:** Toda la información debe representarse de forma explícita como valores en tablas. Ejemplo: `SELECT * FROM Cliente;` debe devolver todos los datos sin estructuras ocultas.

**2. Regla de Acceso Garantizado:** Cada dato debe ser accesible usando nombre de tabla, columna y valor de clave primaria. Ejemplo: `SELECT nombre FROM Cliente WHERE id_cliente=101;`.

**3. Tratamiento Sistemático de Nulos:** Los valores nulos se tratan de forma uniforme en todas las operaciones. Ejemplo: `SELECT * FROM Pedido WHERE fecha_entrega IS NULL;` devuelve los pedidos pendientes.

**4. Catálogo en Línea:** El diccionario de datos debe ser accesible como tablas. Ejemplo: `SELECT table_name FROM information_schema.tables;`.

**5. Sublenguaje Completo:** Debe existir un lenguaje único que permita definir datos, manipularlos, crear vistas, restricciones, seguridad y manejar transacciones. Ejemplo: `CREATE TABLE`, `INSERT`, `UPDATE`, `COMMIT`.

**6. Actualización de Vistas:** Las vistas actualizables deben permitir insertar, actualizar o borrar y reflejar los cambios en las tablas base. Ejemplo: actualizar un `VIEW ClientesMadrid` debe modificar la tabla `Cliente`.

**7. Operaciones de Alto Nivel:** Las operaciones deben trabajar por conjuntos de filas y no fila a fila. Ejemplo: `UPDATE Pedido SET estado='Cerrado' WHERE fecha_pedido<'2024-01-01';`.

**8. Independencia Física:** Cambios en la organización física (índices, ubicación en disco) no deben afectar las aplicaciones. Ejemplo: mover la tabla a otro tablespace no rompe el SQL.

**9. Independencia Lógica:** Cambios en el esquema lógico (agregar columnas, dividir tablas) deben afectar mínimamente las aplicaciones existentes. Ejemplo: agregar una columna `email` no rompe consultas que solo usan `nombre`.

**10. Independencia de Integridad:** Las reglas de integridad deben estar en el catálogo de la BD y no depender de la lógica de la aplicación. Ejemplo: `ALTER TABLE Pedido ADD CONSTRAINT fk_cliente ...;`.

**11. Independencia de Distribución:** La distribución de los datos en múltiples nodos debe ser transparente. Ejemplo: una consulta debe funcionar igual si la tabla está en un servidor o en un clúster distribuido.

**12. No Subversión:** Si existe acceso de bajo nivel (cursores, APIs) no debe ser posible violar las reglas de integridad de la base de datos. Ejemplo: un procedimiento almacenado no puede insertar datos que rompan la foreign key.

**Resumen visual:**

+-------------------------+

No todas las BDs cumplen al 100% las reglas, pero marcan el estándar del modelo relacional.

