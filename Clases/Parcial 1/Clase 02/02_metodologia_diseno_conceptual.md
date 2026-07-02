# Metodología de Diseño Conceptual

- Identificar **entidades** y **atributos**.
- Definir **relaciones** entre entidades.
- Determinar **cardinalidades** (1:1, 1:N, N:M).
- Revisar el modelo con los usuarios para validar requerimientos.

El diseño conceptual asegura que la base de datos refleje correctamente el mundo real.

[Usuario]───<Presta>───[Libro]

Usuario(id_usuario, nombre, email)
Libro(id_libro, titulo, autor)
Prestamo(id_prestamo, fecha, id_usuario, id_libro)

[Cliente]───<Compra>───[Producto]

Cliente(id_cliente, nombre, telefono)
Producto(id_producto, nombre, precio, stock)
Compra(id_compra, fecha, id_cliente, id_producto, cantidad)

[Profesor]───<Imparte>───[Asignatura]───<Matricula>───[Estudiante]

Profesor(id_profesor, nombre, especialidad)
Asignatura(id_asignatura, nombre, creditos)
Estudiante(id_estudiante, nombre, carrera)

