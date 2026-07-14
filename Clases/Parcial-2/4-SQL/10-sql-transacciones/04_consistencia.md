# Consistencia


## Introducción

La segunda propiedad del modelo ACID es la **Consistencia (Consistency)**.

Mientras que la **atomicidad** garantiza que una transacción se ejecute completamente o no se ejecute, la consistencia garantiza que **el estado de la base de datos siga siendo válido antes y después de la transacción**.

En otras palabras, una transacción nunca debe dejar la base de datos en un estado que viole las reglas del negocio o las restricciones definidas en el modelo de datos.

La consistencia no significa que "los datos sean correctos" desde el punto de vista del usuario. Significa que **la base de datos nunca rompe sus propias reglas**.

## ¿Qué significa mantener la consistencia?

Una base de datos consistente es aquella en la que se cumplen simultáneamente todas las restricciones definidas por el diseñador.

Por ejemplo:

- No existen claves primarias duplicadas.
- No existen claves foráneas que apunten a registros inexistentes.
- No existen valores fuera del dominio permitido.
- No existen datos obligatorios con valor NULL.
- No existen saldos imposibles según las reglas del negocio.

Si antes de comenzar una transacción todas esas reglas se cumplían, al finalizar la transacción deben seguir cumpliéndose.

## Un ejemplo sencillo

Supongamos la tabla de cuentas bancarias.

```sql
CREATE TABLE Cuenta (

    IdCuenta INT PRIMARY KEY,

    Titular VARCHAR(100),

    Saldo DECIMAL(10,2)

);
```

Tenemos dos cuentas.

| Cuenta | Saldo |
|---------|-------:|
| Ana | 5000 |
| Luis | 2500 |

Transferimos 800 €.

Estado inicial.

```
5000 + 2500 = 7500 €
```

Después de la transferencia.

```
4200 + 3300 = 7500 €
```

La cantidad total de dinero sigue siendo la misma.

La base de datos continúa siendo consistente.

## Un ejemplo inconsistente

Imaginemos ahora un fallo.

Solo se ejecuta el descuento.

| Cuenta | Saldo |
|---------|-------:|
| Ana | 4200 |
| Luis | 2500 |

Ahora el dinero total es:

```
6700 €
```

Han desaparecido 800 €.

Aunque la sintaxis SQL era correcta, el estado final de la base de datos ya no representa la realidad.

La consistencia se ha perdido.

## La consistencia también depende de las restricciones

Las restricciones que hemos estudiado en clases anteriores forman parte del mecanismo que mantiene la consistencia.

Por ejemplo:

```sql
PRIMARY KEY
```

impide registros duplicados.

```sql
FOREIGN KEY
```

impide referencias inválidas.

```sql
NOT NULL
```

impide datos obligatorios vacíos.

```sql
CHECK
```

(en MySQL 8) permite definir reglas adicionales.

```sql
CHECK (Saldo >= 0)
```

Gracias a estas restricciones el propio SGBD evita que una transacción pueda finalizar en un estado inválido.

## Consistencia y reglas de negocio

No todas las reglas pueden expresarse mediante restricciones SQL.

Por ejemplo:

Un pedido no puede enviarse si todavía no ha sido pagado.

Esta regla pertenece al negocio.

Normalmente se implementa mediante:

- procedimientos almacenados,
- triggers,
- lógica de aplicación,
- validaciones previas.

Las transacciones ayudan a garantizar que todas esas comprobaciones se respeten conjuntamente.

## Otro ejemplo empresarial

Supongamos un almacén.

Tabla Producto.

| Producto | Stock |
|-----------|-------:|
| Portátil | 8 |

Llega un pedido de 3 unidades.

La aplicación realiza:

```sql
UPDATE Producto
SET Stock = Stock - 3
WHERE IdProducto = 12;
```

Si posteriormente ocurre un error y el pedido no llega a registrarse, tendremos:

- stock reducido,
- pedido inexistente.

El inventario deja de representar la realidad.

La consistencia se ha roto.

## ¿Cómo mantiene MySQL la consistencia?

MySQL utiliza varios mecanismos simultáneamente.

Entre ellos:

- restricciones de integridad,
- validaciones,
- control transaccional,
- motor InnoDB,
- bloqueo de registros,
- registro de cambios (Undo Log y Redo Log).

Todos colaboran para asegurar que únicamente puedan confirmarse estados válidos.

## Analogía

Imaginemos un puzle de mil piezas.

Mientras colocamos piezas individuales, el dibujo sigue teniendo sentido.

Pero si intentamos introducir una pieza de otro puzle, inmediatamente deja de encajar.

Las restricciones de la base de datos funcionan igual.

Impiden introducir información incompatible con el resto del modelo.

## Buenas prácticas

- Definir correctamente todas las restricciones posibles.
- No confiar únicamente en la aplicación cliente.
- Validar los datos antes de modificar información.
- Utilizar transacciones en operaciones complejas.
- Diseñar reglas de negocio claramente documentadas.

## Conclusiones

La consistencia garantiza que cada transacción transforme la base de datos desde un estado válido hasta otro estado igualmente válido. Para conseguirlo, el SGBD combina restricciones de integridad, reglas del negocio y mecanismos internos de control. Gracias a ello, los datos mantienen su coherencia incluso cuando múltiples operaciones modifican la información de forma simultánea.

## Ideas clave

- La consistencia mantiene válidas las reglas del modelo.
- Una transacción nunca debe dejar datos imposibles.
- Las restricciones ayudan a preservar la consistencia.
- Las reglas del negocio también forman parte de ella.
- Una base de datos consistente representa correctamente la realidad.

