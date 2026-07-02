* # Ejercicio 3: Plataforma de Bienestar y Belleza

## 1. Lista predefinida de requisitos

1. Los usuarios pueden crear perfiles y seguir rutinas de ejercicio personalizadas.
2. Los entrenadores pueden publicar rutinas y consejos de bienestar.
3. Los usuarios pueden registrar su progreso en rutinas y metas de salud.
4. La plataforma ofrece productos de belleza y bienestar que los usuarios pueden comprar.
5. Los usuarios pueden hacer reseñas y valoraciones de productos y entrenadores.
6. Se pueden generar estadísticas de rendimiento y progreso personal.
7. Existen categorías de rutinas según objetivos: fuerza, cardio, relajación, belleza de piel, cuidado personal.
8. Los usuarios pueden unirse a grupos de interés para compartir consejos y retos.

---

## 2. Identificación de Entidades

* ​**USUARIO**​: persona que usa la plataforma para seguimiento de rutinas, productos y bienestar.
* ​**ENTRENADOR**​: persona que crea rutinas, consejos y programas de bienestar.
* ​**PERFIL**​: información personal, preferencias y objetivos de salud.
* ​**RUTINA**​: conjunto de ejercicios o actividades de bienestar.
* ​**PROGRESO**​: registro de avances y resultados de un usuario.
* ​**PRODUCTO**​: productos de belleza, suplementos o accesorios de bienestar.
* ​**RESEÑA**​: comentarios y valoraciones de productos o entrenadores.
* ​**GRUPO**​: comunidad de usuarios con intereses similares.
* ​**CATEGORIA**​: tipo de rutina o producto (fuerza, cardio, relajación, cuidado personal).

---

## 3. Identificación de Relaciones

* **Usuario — Perfil**
  * `Usuario (1) — tiene — (1) Perfil`
  * Verbo inverso: `Perfil — es de — Usuario`
  * Cardinalidad: **1:1** (Perfil existe por/para Usuario).
  * Nota: implementación física puede ser columna FK en Perfil a Usuario o integrar los campos en Usuario si se prefiere.
* **Usuario — Grupo**
  * `Usuario (0..N) — pertenece a — (1..N) Grupo`
  * Verbo inverso: `Grupo — tiene — Usuario`
  * Cardinalidad: **N:M** (usuario puede estar en muchos grupos; grupo tiene muchos usuarios).
* **Usuario — Progreso**
  * `Usuario (1) — registra — (0..N) Progreso`
  * `Progreso — es registrado por — Usuario`
  * Cardinalidad: **1:N**
* **Usuario — Rutina (seguimiento)**
  * `Usuario (0..N) — sigue — (0..N) Rutina`
  * `Rutina — es seguida por — Usuario`
  * Cardinalidad: **N:M**
* **Entrenador — Rutina (creación)**
  * `Entrenador (1) — crea — (0..N) Rutina`
  * `Rutina — es creada por — Entrenador`
  * Cardinalidad: **1:N**
* **Rutina — Categoria**
  * `Rutina (0..N) — pertenece a — (1) Categoria`
  * `Categoria — agrupa — Rutina`
  * Cardinalidad: **N:1** (una rutina pertenece a una categoría; la categoría agrupa muchas rutinas).
* **Producto — Categoria**
  * `Producto (0..N) — pertenece a — (1) Categoria`
  * `Categoria — contiene — Producto`
  * Cardinalidad: **N:1** (similar a rutinas)
* **Usuario — Producto (compra)**
  * `Usuario (0..N) — compra — (0..N) Producto`
  * `Producto — es comprado por — Usuario`
  * Cardinalidad: **N:M**
* **Usuario — Reseña — Producto/Rutina**
  * `Usuario (1) — escribe — (0..N) Reseña`
  * `Reseña — es escrita por — Usuario`
  * `Reseña — sobre — Producto`**(0..N)**
  * `Reseña — sobre — Rutina`**(0..N)**
  * **Restricción semántica importante:**​**cada `Reseña` debe referenciar exactamente uno** de (`Producto`, `Rutina`)
* **Usuario — Pertenece a Grupo** (ya arriba) — recordatorio N:M.

---

## 4. Identificación de atributos

1. **Usuario** (PK: `id_usuario`)
   * `id_usuario`**(PK)**
   * `nombre`
   * `email`
   * `fecha_nacimiento`
   * `telefono` (opcional)
   * `direccion` (opcional)
2. **Perfil** (PK: `id_perfil`)
   * `id_perfil`**(PK)**
   * `altura`
   * `peso`
   * `objetivos` (texto)
   * `preferencias` (texto / JSON)
   * **Nota:** vínculo 1:1 con `Usuario` (cada usuario tiene un perfil; el perfil no existe sin usuario).
3. **Entrenador** (PK: `id_entrenador`) — rol especializado de `Usuario`
   * `id_entrenador`**(PK)**
   * `id_usuario`**(referencia conceptual a Usuario)**
   * `especialidad`
   * `certificaciones` (lista o texto)
   * `tipo_entrenador` (ej. `personal_trainer`, `nutricionista`, `otro`)
   * `bio` (opcional)
4. **Rutina** (PK: `id_rutina`)
   * `id_rutina`**(PK)**
   * `nombre`
   * `descripcion`
   * `duracion` (minutos)
   * `nivel_dificultad` (ej. básico/intermedio/avanzado)
   * `id_entrenador`**(autor / creador)**
   * `id_categoria` (opcional)
5. **Progreso** (PK: `id_progreso`)
   * `id_progreso`**(PK)**
   * `id_usuario`**(referencia a Usuario)**
   * `id_rutina`**(referencia a Rutina, opcional si el progreso es genérico)**
   * `fecha`
   * `peso` (valor)
   * `repeticiones` (entero, opcional)
   * `notas` (texto)
6. **Producto** (PK: `id_producto`)
   * `id_producto`**(PK)**
   * `nombre`
   * `descripcion`
   * `tipo` (ej. suplemento, accesorio, ropa)
   * `precio`
   * `stock` (opcional)
   * `id_categoria` (categoria del producto)
7. **Categoria** (PK: `id_categoria`)
   * `id_categoria`**(PK)**
   * `nombre`
   * `descripcion`8. **Grupo** (PK: `id_grupo`)
   * `id_grupo`**(PK)**
   * `nombre`
   * `descripcion`8. **Reseña** (PK: `id_resena`)
   * `id_resena`**(PK)**
   * `id_usuario`**(autor — referencia a Usuario)**
   * `contenido`
   * `calificacion` (e.g. 1–5)
   * `fecha`
   * **Vinculación obligatoria a un objetivo:**`id_producto`**OR**`id_rutina`

---

## 5. Jerarquías / Generalizaciones

* USUARIO (generalización) → puede ser ENTRENADOR o CLIENTE (usuario estándar).
* ENTRENADOR → puede ser PERSONAL\_TRAINER o NUTRICIONISTA.

