# Vistas para seguridad

## Introducción

Hasta ahora hemos utilizado las vistas para simplificar consultas. Sin embargo, uno de sus usos más importantes en entornos profesionales es la ​**seguridad**​.

En una empresa no todos los empleados deben tener acceso a toda la información almacenada en la base de datos.

Por ejemplo:

* Recursos Humanos necesita conocer los salarios.
* El departamento comercial no.
* Atención al cliente necesita ver el nombre y el teléfono.
* Contabilidad necesita ver las facturas.
* Un proveedor externo solo debe consultar el catálogo de productos.

Las vistas permiten mostrar únicamente la información que cada usuario necesita.

---

## El problema

Supongamos la siguiente tabla:

```text
Empleado
```

| IdEmpleado | Nombre | Cargo | Salario | Dirección | Teléfono |
| -----------: | -------- | ------- | --------: | ------------ | ----------- |

Si concedemos acceso directo a esta tabla, el usuario podrá consultar todas las columnas.

```sql
SELECT *
FROM Empleado;
```

El resultado incluiría información sensible como:

* salarios;
* direcciones;
* teléfonos.

En muchas situaciones esto no es aceptable.

---

## Crear una vista segura

Podemos construir una vista que únicamente muestre la información necesaria.

```sql
CREATE VIEW VistaEmpleadosPublica AS
SELECT
    IdEmpleado,
    Nombre,
    Cargo
FROM Empleado;
```

Ahora el usuario consultará:

```sql
SELECT *
FROM VistaEmpleadosPublica;
```

Y únicamente obtendrá:

| IdEmpleado | Nombre | Cargo |
| -----------: | -------- | ------- |

Las columnas sensibles permanecen ocultas.

---

## Otro ejemplo

Supongamos la tabla:

```text
Cliente
```

Contiene:

* nombre;
* email;
* teléfono;
* dirección;
* fecha de nacimiento.

Un departamento de marketing solo necesita:

```sql
CREATE VIEW VistaMarketingClientes AS
SELECT
    IdCliente,
    Nombre,
    Email
FROM Cliente;
```

La información personal permanece protegida.

---

## Seguridad mediante permisos

Las vistas suelen combinarse con el sistema de permisos del SGBD.

Una estrategia habitual consiste en:

* denegar el acceso directo a las tablas;
* conceder acceso únicamente a determinadas vistas.

Esquema:

```text
Usuario

↓

Vista

↓

Tabla
```

El usuario nunca accede directamente a las tablas originales.

---

## Ventajas

Este enfoque ofrece varias ventajas:

* protege información confidencial;
* reduce errores accidentales;
* simplifica el cumplimiento de normativas de protección de datos;
* facilita la administración de permisos.

En organizaciones grandes este patrón es extremadamente habitual.

---

## ¿Es suficiente una vista para garantizar la seguridad?

No.

Las vistas son una herramienta muy útil, pero deben complementarse con:

* usuarios;
* roles;
* permisos (`GRANT` y `REVOKE`);
* políticas de acceso.

Estos temas se estudiarán más adelante en el curso.

La vista limita la información disponible, pero el control real del acceso depende del sistema de permisos del SGBD.

---

## Buenas prácticas

Cuando una vista tenga fines de seguridad conviene:

* mostrar únicamente las columnas necesarias;
* evitar incluir datos personales innecesarios;
* utilizar nombres descriptivos;
* documentar claramente su finalidad;
* combinarla con una correcta gestión de permisos.

---

## Ideas clave

* Las vistas permiten ocultar columnas sensibles.
* Son una herramienta muy utilizada para mejorar la seguridad.
* Es posible conceder acceso a una vista sin conceder acceso a la tabla original.
* Deben combinarse con usuarios y permisos para ofrecer una protección completa.
* Constituyen una buena práctica en aplicaciones empresariales.

