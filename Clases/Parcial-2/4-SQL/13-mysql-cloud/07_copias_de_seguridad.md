# Copias de seguridad

## Introducción

Durante todo el curso hemos insistido en que la información constituye uno de los activos más valiosos de cualquier organización.

Perder una base de datos puede significar:

- pérdida de clientes,
- pérdida de pedidos,
- desaparición de información financiera,
- incumplimiento de obligaciones legales,
- daños económicos y reputacionales.

Por este motivo, ninguna estrategia profesional de administración de bases de datos está completa sin un sistema de copias de seguridad.

En los servicios cloud, las copias de seguridad forman parte de las funcionalidades más importantes ofrecidas por los proveedores.

## ¿Qué es una copia de seguridad?

Una copia de seguridad (backup) es una réplica de la información que permite restaurar la base de datos en caso de pérdida o corrupción de los datos originales.

Su objetivo principal consiste en recuperar la información cuando ocurre un incidente.

Es importante destacar que una copia de seguridad **no está pensada para sustituir la base de datos en funcionamiento**, sino para recuperar información cuando sea necesario.

## ¿Por qué pueden perderse los datos?

Existen muchas causas posibles.

### Error humano

Un administrador elimina accidentalmente una tabla.

```sql
DROP TABLE Pedido;
```

### Error de una aplicación

Un programa defectuoso actualiza miles de registros con valores incorrectos.

### Ataques informáticos

Un atacante modifica o elimina información.

### Corrupción lógica

La información sigue existiendo físicamente, pero contiene datos incorrectos.

### Fallos de hardware

Aunque menos frecuentes en la nube, siguen siendo posibles.

## Copias automáticas

Una de las grandes ventajas de servicios como Amazon RDS y Google Cloud SQL consiste en que pueden generar copias de seguridad automáticamente.

Normalmente el administrador configura aspectos como:

- horario,
- frecuencia,
- periodo de retención.

El resto del proceso queda automatizado.

## Restauración

Una copia únicamente resulta útil si puede restaurarse correctamente.

Los proveedores cloud suelen permitir recuperar:

- toda la base de datos,
- una nueva instancia creada a partir de una copia,
- o el estado existente en un momento determinado, dependiendo del servicio contratado.

Esta capacidad reduce enormemente el tiempo necesario para recuperar un sistema.

## Punto de recuperación

Imaginemos que un usuario elimina información a las 10:30.

Si existe una copia realizada a las 03:00, quizá sea necesario perder varias horas de trabajo.

Algunos servicios permiten restaurar la base de datos a un instante muy próximo al momento del incidente mediante mecanismos de recuperación temporal.

Cuanto menor sea la pérdida de información aceptable, mayores serán normalmente los requisitos técnicos y económicos.

## ¿Dónde deben almacenarse?

Una buena copia de seguridad debe almacenarse separada del sistema principal.

Si la copia se encuentra exactamente en el mismo servidor y este sufre una avería grave, ambas podrían perderse simultáneamente.

Los proveedores cloud suelen almacenar las copias en infraestructuras independientes diseñadas específicamente para este propósito.

## ¿Basta con confiar en las copias automáticas?

No siempre.

Muchas organizaciones mantienen además estrategias propias.

Por ejemplo:

- exportaciones periódicas,
- almacenamiento en otra región,
- conservación de copias durante varios años,
- verificación periódica de la posibilidad de restauración.

Esto aumenta la resiliencia frente a distintos tipos de incidentes.

## Caso práctico

Un desarrollador de TechShop ejecuta accidentalmente:

```sql
DELETE FROM Pedido;
```

sin incluir una cláusula `WHERE`.

Miles de pedidos desaparecen.

Gracias a las copias automáticas configuradas en el servicio cloud, la empresa puede restaurar la información hasta un instante inmediatamente anterior al error.

La interrupción del servicio se reduce considerablemente.

## Buenas prácticas

- Configurar copias automáticas desde el primer día.
- Definir claramente el periodo de retención.
- Probar regularmente la restauración.
- Mantener copias independientes cuando sea necesario.
- No confiar únicamente en que las copias existen: comprobar que realmente pueden recuperarse.

## Conclusiones

Las copias de seguridad constituyen uno de los mecanismos más importantes para proteger la información de una organización. Los servicios cloud facilitan enormemente su automatización, pero la responsabilidad de definir una estrategia adecuada continúa siendo de la empresa. Una copia que nunca se ha probado puede no ser útil cuando realmente se necesite.

## Ideas clave

- Las copias de seguridad permiten recuperar información perdida.
- Los errores humanos siguen siendo una de las principales causas de pérdida de datos.
- AWS RDS y Google Cloud SQL automatizan gran parte del proceso.
- Restaurar correctamente es tan importante como realizar la copia.
- Una estrategia profesional incluye planificación, pruebas y verificación periódica.

