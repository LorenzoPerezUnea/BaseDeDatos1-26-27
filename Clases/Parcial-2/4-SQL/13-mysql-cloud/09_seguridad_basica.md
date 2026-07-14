# Seguridad básica

## Introducción

Una base de datos puede contener algunos de los activos más valiosos de una organización:

- información de clientes,
- contraseñas cifradas,
- datos financieros,
- historiales médicos,
- pedidos,
- facturación,
- información estratégica.

Por ello, proteger una base de datos constituye una de las responsabilidades más importantes de cualquier equipo de desarrollo y administración.

Cuando utilizamos un servicio cloud como Amazon RDS o Google Cloud SQL, parte de la infraestructura está protegida por el proveedor.

Sin embargo, esto **no significa que la seguridad quede completamente resuelta**.

El cliente continúa siendo responsable de numerosas decisiones relacionadas con la protección de la información.

## El modelo de responsabilidad compartida

Los grandes proveedores cloud utilizan un principio denominado **modelo de responsabilidad compartida**.

De forma simplificada:

### El proveedor protege

- Centros de datos.
- Hardware.
- Redes físicas.
- Alimentación eléctrica.
- Infraestructura básica.
- Disponibilidad de la plataforma.

### El cliente protege

- Usuarios.
- Contraseñas.
- Permisos.
- Aplicaciones.
- Consultas SQL.
- Diseño de la base de datos.
- Información almacenada.

Este reparto resulta fundamental para comprender cómo funciona la seguridad en la nube.

## Control de acceso

El primer mecanismo de protección consiste en impedir que cualquier persona pueda acceder a la base de datos.

Para ello se utilizan usuarios con autenticación.

Por ejemplo:

```sql
CREATE USER 'analista'
IDENTIFIED BY 'ContraseñaSegura';
```

Posteriormente se asignan únicamente los permisos necesarios.

```sql
GRANT SELECT
ON TechShop.*
TO 'analista';
```

Este principio recibe el nombre de **mínimo privilegio**.

Cada usuario debe disponer exclusivamente de los permisos imprescindibles para realizar su trabajo.

## Redes seguras

No todas las aplicaciones deberían poder conectarse libremente a una base de datos.

Los servicios cloud permiten restringir el acceso mediante:

- redes privadas,
- direcciones IP autorizadas,
- reglas de firewall,
- grupos de seguridad.

Esto reduce considerablemente la superficie de ataque.

## Cifrado

Otra medida habitual consiste en utilizar conexiones cifradas entre la aplicación y la base de datos.

De esta forma, si un atacante intercepta la comunicación, la información no podrá interpretarse fácilmente.

Además, muchos proveedores permiten cifrar también los datos almacenados en disco.

## Actualizaciones

Mantener el software actualizado resulta esencial para corregir vulnerabilidades conocidas.

Los servicios administrados facilitan enormemente esta tarea al automatizar gran parte del proceso de actualización de la infraestructura.

Aun así, la empresa debe planificar cuidadosamente cuándo aplicar determinadas actualizaciones para minimizar el impacto sobre la aplicación.

## Auditoría y monitorización

La seguridad no consiste únicamente en impedir accesos.

También es importante detectar comportamientos anómalos.

Por ejemplo:

- intentos repetidos de autenticación,
- incremento inusual de consultas,
- accesos desde ubicaciones inesperadas,
- modificaciones masivas de información.

La monitorización continua permite reaccionar rápidamente ante posibles incidentes.

## Errores frecuentes

Uno de los problemas más habituales consiste en pensar que utilizar un servicio cloud elimina todas las responsabilidades relacionadas con la seguridad.

Esto es incorrecto.

Algunos errores muy comunes son:

- utilizar contraseñas débiles,
- conceder privilegios excesivos,
- compartir cuentas entre varios usuarios,
- exponer la base de datos directamente a Internet,
- no revisar periódicamente los permisos.

En la mayoría de los casos, estos problemas no dependen del proveedor, sino de una configuración inadecuada.

## Caso práctico

TechShop crea una nueva base de datos en la nube.

En lugar de utilizar un único usuario administrador para toda la aplicación, decide crear distintos perfiles:

- administrador,
- desarrollador,
- analista,
- aplicación web.

Cada uno dispone únicamente de los permisos necesarios para realizar sus funciones.

Esta estrategia reduce considerablemente el impacto que tendría el compromiso de una cuenta.

## Buenas prácticas

- Aplicar el principio de mínimo privilegio.
- Utilizar contraseñas robustas.
- Revisar periódicamente los permisos concedidos.
- Restringir el acceso mediante redes seguras.
- Utilizar conexiones cifradas.
- Supervisar continuamente la actividad de la base de datos.
- Mantener actualizada la infraestructura.

## Conclusiones

La seguridad de una base de datos cloud es una responsabilidad compartida entre el proveedor y la organización. Aunque servicios como Amazon RDS y Google Cloud SQL protegen la infraestructura física, corresponde al cliente configurar correctamente usuarios, permisos, accesos y políticas de protección de la información. Una estrategia de seguridad eficaz combina tecnología, buenas prácticas y supervisión continua.

## Ideas clave

- La seguridad no desaparece por utilizar servicios cloud.
- El proveedor protege la infraestructura; el cliente protege los datos.
- El principio de mínimo privilegio reduce riesgos.
- Las redes seguras y el cifrado son mecanismos fundamentales.
- La monitorización continua permite detectar incidentes antes de que produzcan daños importantes.

