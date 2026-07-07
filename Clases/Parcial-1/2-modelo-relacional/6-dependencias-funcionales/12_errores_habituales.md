# Errores habituales

Las dependencias funcionales constituyen uno de los conceptos más abstractos del Modelo Relacional. Por este motivo, es completamente normal cometer errores durante las primeras etapas de aprendizaje.

La buena noticia es que la mayoría de estos errores siguen patrones muy similares.

Aprender a reconocerlos ayudará a evitarlos cuando diseñemos bases de datos reales.

### Error 1. Confundir los datos con las reglas del negocio

Este es, probablemente, el error más frecuente.

Supongamos la siguiente tabla.

| Ciudad      | Provincia |
| ------------- | ----------- |
| Santander   | Cantabria |
| Torrelavega | Cantabria |

Al observar únicamente estos datos, un estudiante podría pensar que:

```text
Provincia → Ciudad
```

porque todas las filas muestran una única ciudad por provincia.

Sin embargo, sabemos que Cantabria posee numerosos municipios.

La dependencia correcta es:

```text
Ciudad → Provincia
```

Las dependencias deben deducirse del negocio, no de una muestra de datos.

### Error 2. Suponer que toda clave es primaria

Una tabla puede poseer varias claves candidatas.

Por ejemplo:

```text
IdEmpleado

DNI

CorreoCorporativo
```

Las tres pueden identificar unívocamente a un empleado.

Solo una será elegida como clave primaria.

Las demás seguirán siendo claves candidatas.

### Error 3. Confundir dependencia con asociación

Muchos estudiantes creen que dos atributos relacionados implican automáticamente una dependencia funcional.

Por ejemplo:

```text
Cliente

Pedido
```

Existe una relación entre ambos conceptos.

Sin embargo:

```text
Cliente → Pedido
```

no es una dependencia funcional.

Un cliente puede realizar muchos pedidos.

Conocer el cliente no permite identificar un pedido concreto.

### Error 4. Ignorar las claves compuestas

Otro error frecuente consiste en analizar únicamente atributos individuales.

Consideremos:

```text
(IdPedido, IdProducto)
→ Cantidad
```

Algunos estudiantes intentan simplificarla.

```text
IdPedido → Cantidad
```

o bien

```text
IdProducto → Cantidad
```

Ninguna de las dos es correcta.

Es necesaria la combinación de ambos atributos.

### Error 5. No comprobar la minimalidad

Encontrar un conjunto que determine todos los atributos no es suficiente.

También debemos comprobar que ningún atributo sobra.

Por ejemplo:

```text
(IdCliente, Nombre)
```

Si:

```text
IdCliente+
```

ya determina toda la tabla, entonces **Nombre** es innecesario.

La clave no es mínima.

### Error 6. Memorizar en lugar de razonar

Las dependencias funcionales no deben memorizarse.

Siempre deben deducirse a partir del funcionamiento del negocio.

Un buen diseñador no recuerda listas de dependencias.

Las descubre analizando cuidadosamente el dominio del problema.

### Consejos para evitarlos

Antes de aceptar cualquier dependencia funcional, conviene hacerse estas preguntas.

* ¿Es una regla del negocio?
* ¿Siempre será cierta?
* ¿Depende realmente de todos los atributos de la izquierda?
* ¿Existe algún contraejemplo?
* ¿Estoy utilizando una muestra de datos demasiado pequeña?

Responderlas ayuda a detectar la mayoría de los errores.

### Ideas clave

* Las dependencias funcionales se deducen del negocio, no de los datos.
* No todas las relaciones entre atributos son dependencias funcionales.
* Las claves candidatas deben ser mínimas.
* Las claves compuestas requieren un análisis conjunto.
* Razonar siempre produce mejores resultados que memorizar.

