# Carga de datos

## Introducción

Una base de datos recién creada contiene únicamente la estructura definida mediante tablas, restricciones e índices.

Aunque el esquema sea correcto, todavía no resulta útil para desarrollar consultas, comprobar el funcionamiento de la aplicación o analizar el rendimiento.

Por este motivo, la siguiente fase del proyecto consiste en **cargar datos iniciales**.

En entornos profesionales este proceso recibe distintos nombres:

- carga inicial;
- datos semilla (*seed data*);
- población de la base de datos;
- datos de prueba.

Estos datos permiten comenzar el desarrollo de la aplicación incluso antes de disponer de información real procedente de clientes.

En este bloque construiremos un conjunto de datos suficientemente amplio y coherente para poder realizar todos los ejercicios posteriores del taller.

## Objetivos del bloque

Al finalizar este bloque el estudiante será capaz de:

- Diseñar una estrategia de carga de datos.
- Respetar las dependencias entre tablas.
- Insertar información coherente.
- Detectar errores derivados de claves foráneas.
- Preparar una base de datos para realizar pruebas.

## Orden de carga

Uno de los errores más frecuentes consiste en insertar información sin respetar las dependencias existentes entre tablas.

Por ejemplo, no es posible registrar un pedido si todavía no existe el cliente al que pertenece.

Por ello seguiremos el siguiente orden.

1. Departamento
2. Empleado
3. Categoría
4. Proveedor
5. Producto
6. ProductoProveedor
7. Cliente
8. Dirección
9. Pedido
10. DetallePedido
11. Pago
12. Envío

Este orden evita la mayoría de los errores relacionados con claves foráneas.

## Tamaño del conjunto de datos

Para que las consultas resulten interesantes, utilizaremos un volumen de información superior al estrictamente necesario.

Se recomienda, como mínimo:

| Tabla | Registros aproximados |
|--------|----------------------:|
| Departamento | 8 |
| Empleado | 40 |
| Categoría | 20 |
| Proveedor | 30 |
| Producto | 300 |
| Cliente | 500 |
| Dirección | 700 |
| Pedido | 2000 |
| DetallePedido | 7000 |
| Pago | 2000 |
| Envío | 2000 |

Estas cifras permiten obtener resultados variados en prácticamente todos los ejercicios del taller.

## Características de los datos

Los datos deben parecer reales.

No es recomendable utilizar únicamente registros como:

```text
Cliente 1

Cliente 2

Producto A

Producto B
```

Es preferible emplear nombres plausibles.

Por ejemplo:

```text
Ana López

Carlos Martínez

SSD Samsung 1 TB

Monitor LG 27"

Teclado Mecánico RGB
```

Una base de datos con datos realistas facilita detectar problemas de diseño y mejora la comprensión de los ejercicios.

## Coherencia entre tablas

Toda la información debe ser consistente.

Por ejemplo:

- ningún pedido debe pertenecer a un cliente inexistente;
- todos los productos deben pertenecer a una categoría;
- ningún pago puede asociarse a un pedido inexistente;
- un envío debe corresponder exactamente a un pedido registrado.

Mantener esta coherencia resulta tan importante como insertar los propios datos.

## Ejercicio guiado 1 (Profesor)

Crear datos para las siguientes tablas:

- Departamento
- Empleado

El profesor explicará el orden de inserción y comprobará la integridad de los datos.

## Ejercicio guiado 2 (Profesor)

Insertar:

- cinco categorías;
- diez productos;
- tres proveedores.

Posteriormente comprobar que todas las relaciones funcionan correctamente.

## Ejercicios de aula

### Ejercicio 1

Genera diez departamentos diferentes.

### Ejercicio 2

Genera cincuenta empleados distribuidos entre los departamentos.

### Ejercicio 3

Diseña veinte categorías de productos.

### Ejercicio 4

Genera treinta proveedores distintos.

### Ejercicio 5

Inserta cien productos diferentes.

### Ejercicio 6

Registra cien clientes.

### Ejercicio 7

Añade al menos una dirección para cada cliente.

### Ejercicio 8

Genera doscientos pedidos distribuidos entre distintos clientes.

### Ejercicio 9

Asigna entre uno y cinco productos a cada pedido.

### Ejercicio 10

Registra pagos y envíos para todos los pedidos.

## Retos

### Reto 1

Diseña un conjunto de datos donde algunos productos no tengan existencias.

### Reto 2

Genera pedidos con distintos estados.

Ejemplo:

- Pendiente.
- Preparación.
- Enviado.
- Entregado.
- Cancelado.

### Reto 3

Introduce deliberadamente algunos errores y comprueba cómo responde MySQL cuando se incumplen las restricciones de integridad.

## Trabajo autónomo

1. Ampliar el número de clientes hasta 500.
2. Alcanzar al menos 300 productos.
3. Generar un mínimo de 2.000 pedidos.
4. Verificar todas las claves foráneas.
5. Comprobar que no existen registros huérfanos.

## Lista de comprobación

Antes de continuar asegúrate de que:

- Todas las tablas contienen datos.
- No existen errores de integridad referencial.
- Los datos parecen realistas.
- Hay suficiente volumen para realizar consultas complejas.
- El conjunto de datos resulta coherente.

## Conclusiones

Una base de datos correctamente poblada permite validar el diseño, desarrollar consultas complejas y detectar errores antes de que la aplicación entre en producción. La calidad de los datos de prueba influye directamente en la utilidad del resto del taller.

