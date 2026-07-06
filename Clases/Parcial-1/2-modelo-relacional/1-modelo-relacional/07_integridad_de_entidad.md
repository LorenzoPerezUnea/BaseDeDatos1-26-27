# Integridad de entidad

Una base de datos no solo debe almacenar información.

También debe garantizar que esa información sea correcta.

El Modelo Relacional incorpora una serie de reglas cuyo objetivo consiste en preservar la calidad de los datos. Estas reglas reciben el nombre de ​**restricciones de integridad**​.

La primera de ellas es la ​**integridad de entidad**​.

### ¿Qué significa "integridad"?

En informática, la palabra **integridad** hace referencia a la consistencia y validez de la información.

Una base de datos íntegra es aquella cuyos datos respetan las reglas definidas durante el diseño.

Cuando estas reglas se incumplen, comienzan a aparecer registros ambiguos, relaciones rotas y errores difíciles de detectar.

### La regla de integridad de entidad

La integridad de entidad establece que:

> **Toda relación debe poseer una clave primaria cuyos valores sean únicos y nunca nulos.**

Esta regla parece sencilla, pero resulta imprescindible.

Si una tabla permitiera registros sin identificador, sería imposible distinguir unos de otros.

### ¿Por qué no puede ser nula?

Supongamos la siguiente tabla.

| IdCliente | Nombre |
| ----------: | -------- |
|         1 | Ana    |
|      NULL | Carlos |
|      NULL | Marta  |

¿Qué ocurriría si deseáramos modificar el segundo registro?

No podríamos identificarlo de forma inequívoca.

La clave primaria dejaría de cumplir su función.

Por este motivo, los valores nulos están prohibidos en las claves primarias.

### ¿Por qué no puede repetirse?

Consideremos ahora otra situación.

| IdCliente | Nombre |
| ----------: | -------- |
|         5 | Ana    |
|         5 | Carlos |

¿Cuál de los dos clientes corresponde realmente al identificador 5?

No existe forma de saberlo.

La base de datos ha perdido la capacidad de identificar unívocamente cada registro.

Por ello tampoco se permiten valores duplicados.

### Cómo lo garantiza MySQL

Cuando más adelante creemos tablas en MySQL utilizaremos la restricción:

```sql
PRIMARY KEY
```

El propio servidor impedirá automáticamente insertar registros que incumplan esta regla.

De esta forma el SGBD ayuda a mantener la integridad de la información.

### Caso práctico

En nuestra empresa comercial, todos los clientes tendrán un identificador único.

Aunque dos personas compartan nombre, apellidos y ciudad, siempre existirán dos claves primarias diferentes.

Esto permitirá distinguir claramente cada cliente y evitar confusiones durante el procesamiento de pedidos o facturas.

### Ideas clave

* La integridad de entidad garantiza que cada registro pueda identificarse de forma única.
* Toda relación debe disponer de una clave primaria.
* Una clave primaria nunca puede ser nula.
* Una clave primaria nunca puede repetirse.
* MySQL aplica automáticamente esta restricción cuando definimos una clave primaria.

