# Casos reales

Hasta ahora hemos trabajado principalmente con ejemplos sencillos para comprender cada concepto por separado.

Sin embargo, los proyectos profesionales suelen combinar simultáneamente entidades, relaciones, cardinalidades y numerosas reglas de negocio.

En este capítulo analizaremos algunos ejemplos reales para comprobar cómo se aplican todos estos conceptos conjuntamente.

### Caso 1. Comercio electrónico

Un sistema de venta por Internet suele incluir entidades como:

* Cliente
* Pedido
* Producto
* Pago
* Envío

Entre ellas aparecen relaciones como:

```mermaid
erDiagram

CLIENTE ||--o{ PEDIDO : realiza

PEDIDO ||--|| PAGO : genera

PEDIDO ||--|| ENVIO : produce

PEDIDO }o--o{ PRODUCTO : contiene
```

Este modelo representa únicamente una parte del sistema, pero ya permite comprender el funcionamiento básico del negocio.

### Caso 2. Universidad

En una universidad encontramos entidades como:

* Estudiante
* Asignatura
* Profesor
* Matrícula

El análisis revela rápidamente una relación muchos a muchos entre estudiantes y asignaturas.

En lugar de mantenerla directamente, se crea una entidad **Matrícula** que almacena además información como:

* Curso académico.
* Convocatoria.
* Calificación.

Observamos nuevamente cómo una entidad asociativa representa un hecho real del negocio.

### Caso 3. Hospital

Un hospital puede modelarse mediante entidades como:

* Paciente
* Médico
* Consulta
* Receta

Las reglas de negocio indican, por ejemplo:

* Un paciente puede acudir a muchas consultas.
* Cada consulta pertenece a un único paciente.
* Una consulta puede generar varias recetas.

Estas reglas determinan las cardinalidades del modelo.

### Nuestro caso de estudio

La empresa comercial que estamos desarrollando seguirá exactamente la misma metodología.

En cada nueva clase iremos incorporando nuevas entidades y restricciones.

Al finalizar el semestre el modelo será comparable, en complejidad, al de muchas aplicaciones empresariales reales.

### ¿Qué tienen en común todos estos modelos?

Aunque pertenezcan a sectores diferentes, todos comparten una misma filosofía:

* Identificar correctamente las entidades.
* Descubrir las reglas del negocio.
* Definir las cardinalidades.
* Evitar redundancias.
* Garantizar la integridad de los datos.

El lenguaje del negocio cambia.

Los principios del diseño permanecen prácticamente iguales.

### Ideas clave

* Los mismos principios se aplican en cualquier dominio.
* Las reglas del negocio determinan el modelo conceptual.
* Las entidades asociativas aparecen con frecuencia en proyectos reales.
* Analizar ejemplos variados ayuda a desarrollar criterio de diseño.
* Un buen modelo conceptual es independiente del tipo de organización.

