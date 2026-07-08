# Caso completo paso a paso

A lo largo de esta clase hemos estudiado las distintas Formas Normales por separado. Para finalizar, recorreremos el proceso completo utilizando nuestro caso de estudio de la empresa comercial.

### Paso 1. El diseño inicial

Supongamos que comenzamos con la siguiente tabla.

| Pedido | Cliente | Dirección | Producto | Categoría | Precio | Cantidad |
| -------: | --------- | ------------ | ---------- | ------------ | -------: | ---------: |

Aunque parece sencilla, mezcla información de varias entidades diferentes.

Además, muchos datos se repetirán continuamente.

### Paso 2. Analizar las dependencias

Podemos identificar dependencias como:

```text
IdPedido → IdCliente

IdCliente → Dirección

IdProducto → Precio

IdProducto → Categoría

IdCategoria → NombreCategoria
```

Estas dependencias nos indican que existen atributos que realmente pertenecen a otras entidades.

### Paso 3. Aplicar la Primera Forma Normal

Comprobamos que cada columna contiene valores atómicos.

Si existieran listas de productos o varios teléfonos en una misma celda, deberíamos dividirlos en nuevas tablas.

Una vez eliminados esos grupos repetitivos, el modelo cumple la 1FN.

### Paso 4. Aplicar la Segunda Forma Normal

Analizamos las claves compuestas.

En la tabla LINEAPEDIDO detectamos que:

```text
IdProducto → Precio
```

El precio depende únicamente del producto.

Debe trasladarse a la tabla PRODUCTO.

### Paso 5. Aplicar la Tercera Forma Normal

Observamos que:

```text
IdCategoria → NombreCategoria
```

Por tanto, el nombre de la categoría no pertenece realmente a PRODUCTO.

Creamos la tabla:

```text
CATEGORIA

IdCategoria
NombreCategoria
```

### Paso 6. Resultado final

El modelo queda formado por varias tablas relacionadas.

```text
CLIENTE

PRODUCTO

CATEGORIA

PEDIDO

LINEAPEDIDO
```

Cada entidad almacena únicamente su propia información.

Las redundancias desaparecen y el diseño resulta mucho más fácil de mantener.

### Lo aprendido

Este proceso resume la filosofía de la normalización.

No consiste simplemente en dividir tablas.

Consiste en analizar cuidadosamente las dependencias funcionales y decidir cuál es el lugar correcto para cada dato.

### Ideas clave

* La normalización es un proceso progresivo.
* Cada Forma Normal elimina un tipo específico de problema.
* Las dependencias funcionales guían todas las decisiones.
* El resultado es un modelo más consistente y fácil de mantener.
* Nuestro caso de estudio continuará utilizándose durante las próximas clases para implementar este modelo en MySQL.

