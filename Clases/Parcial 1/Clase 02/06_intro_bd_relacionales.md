# Introducción a Bases de Datos Relacionales

- Conjunto de tablas relacionadas mediante claves.
- Cumplen con principios del modelo relacional de Codd.
- Ventajas:
  - Organización estructurada.
  - Eliminación de redundancia.
  - Integridad y consistencia.
- Ejemplos: MySQL, PostgreSQL, Oracle, SQL Server.

Son el estándar de facto para aplicaciones empresariales y académicas.

Implementación de una relación N:M en modelo relacional

```
Tabla CLIENTE                Tabla PRODUCTO
id_cliente (PK)              id_producto (PK)
nombre                       nombre

        ↓   relación N:M   ↓

          Tabla COMPRA
          id_cliente (FK)
          id_producto (FK)
          fecha
```
