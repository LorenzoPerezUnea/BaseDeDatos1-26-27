# Durabilidad

## Introducción

La cuarta y última propiedad del modelo ACID es la **Durabilidad (Durability)**.

Hasta ahora hemos aprendido que una transacción debe ejecutarse completamente (Atomicidad), mantener la base de datos en un estado válido (Consistencia) y evitar interferencias entre usuarios concurrentes (Aislamiento).

Sin embargo, aún queda una pregunta fundamental.

¿Qué ocurre cuando una transacción ya ha finalizado correctamente y, apenas un segundo después, el servidor pierde la alimentación eléctrica?

¿Se conservan los datos?

¿Se pierde todo el trabajo realizado?

La propiedad de durabilidad responde precisamente a estas preguntas.

Una vez que una transacción ha sido confirmada mediante `COMMIT`, sus cambios deben permanecer almacenados de forma permanente, incluso si el sistema experimenta un fallo inmediatamente después.

Esta garantía es esencial en cualquier sistema crítico, ya que los usuarios necesitan confiar en que una operación confirmada nunca desaparecerá.

## ¿Qué significa que un dato sea duradero?

Cuando ejecutamos una transacción correctamente y finalizamos con:

```sql
COMMIT;
```

MySQL garantiza que los cambios pasarán a formar parte permanente de la base de datos.

Esto significa que, aunque ocurra cualquiera de las siguientes situaciones:

- Corte del suministro eléctrico.
- Reinicio inesperado del servidor.
- Bloqueo del sistema operativo.
- Caída del servicio MySQL.
- Reinicio del ordenador.
- Fallo de la aplicación cliente.

los cambios confirmados seguirán existiendo cuando el sistema vuelva a estar operativo.

## ¿Por qué es necesaria esta propiedad?

Imaginemos una tienda online.

Un cliente realiza un pedido y efectúa un pago mediante tarjeta.

Internamente ocurre lo siguiente:

- Se registra el pedido.
- Se genera la factura.
- Se descuenta el stock.
- Se registra el pago.
- Se ejecuta `COMMIT`.

Justo después del `COMMIT`, el servidor sufre un apagón.

Cuando el sistema vuelve a arrancar, el cliente espera que:

- Su pedido siga existiendo.
- El pago continúe registrado.
- El inventario permanezca actualizado.

Si alguno de esos datos hubiese desaparecido, el sistema habría perdido información crítica.

## ¿Cómo consigue MySQL la durabilidad?

Guardar información únicamente en memoria RAM sería insuficiente.

La memoria principal es volátil.

Cuando el equipo pierde alimentación, su contenido desaparece.

Por ello, antes de considerar una transacción como confirmada, MySQL utiliza mecanismos adicionales para asegurar que la información pueda recuperarse posteriormente.

Entre ellos destacan:

- Escritura en disco.
- Redo Log.
- Buffer Pool.
- Checkpoints.
- Recuperación automática tras fallos.

Estos mecanismos permiten reconstruir el estado correcto de la base de datos incluso después de un apagón inesperado.

## El Redo Log

Uno de los componentes más importantes del motor InnoDB es el **Redo Log**.

Antes de que una modificación llegue definitivamente a los archivos de datos, MySQL registra la operación en este archivo especial.

De esta manera, si el sistema falla antes de completar la escritura definitiva, durante el siguiente arranque podrá reproducir todas las operaciones pendientes.

Conceptualmente el proceso es similar al siguiente:

```
Modificar datos

↓

Registrar cambio en Redo Log

↓

Confirmar COMMIT

↓

Escribir definitivamente en disco
```

Si el servidor se apaga entre los dos últimos pasos, el Redo Log permitirá completar la operación posteriormente.

## Ejemplo

Supongamos la siguiente transacción.

```sql
START TRANSACTION;

UPDATE Cuenta
SET Saldo = Saldo - 1000
WHERE IdCuenta = 1;

UPDATE Cuenta
SET Saldo = Saldo + 1000
WHERE IdCuenta = 2;

COMMIT;
```

El usuario recibe el mensaje:

```
Query OK.
```

A los pocos milisegundos se produce un corte eléctrico.

Cuando MySQL vuelva a iniciarse, utilizará la información registrada para garantizar que ambas actualizaciones permanezcan almacenadas.

## Analogía

Pensemos en una notaría.

Cuando una escritura queda firmada e inscrita oficialmente, ya no depende de que el notario recuerde el contenido.

Existe un registro permanente que permite recuperarla incluso muchos años después.

El Redo Log cumple una función parecida.

Actúa como un registro oficial de los cambios ya confirmados.

## ¿Puede perderse información?

Sí, pero únicamente si la transacción todavía no había sido confirmada.

Mientras una transacción permanece abierta:

```sql
START TRANSACTION;
```

sus modificaciones siguen siendo temporales.

Solo el `COMMIT` convierte esos cambios en permanentes.

## Buenas prácticas

- Confirmar únicamente cuando toda la operación haya finalizado correctamente.
- Evitar mantener transacciones abiertas durante largos periodos.
- Realizar copias de seguridad periódicas.
- Supervisar el estado del almacenamiento físico.
- Utilizar motores transaccionales como InnoDB.

## Conclusiones

La durabilidad garantiza que una vez confirmada una transacción, sus efectos permanecerán almacenados de forma permanente. Gracias a mecanismos internos como el Redo Log y la recuperación automática, MySQL puede soportar fallos inesperados sin perder operaciones ya confirmadas.

## Ideas clave

- Una transacción confirmada nunca debe perderse.
- El `COMMIT` marca el momento en que los cambios pasan a ser permanentes.
- MySQL utiliza registros especiales para asegurar la recuperación.
- La durabilidad protege la información frente a fallos del sistema.
- Es la cuarta propiedad del modelo ACID.

