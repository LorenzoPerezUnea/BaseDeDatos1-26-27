# CHECK

## Introducción

Hasta ahora hemos utilizado restricciones que controlan la existencia o la unicidad de los datos.

Sin embargo, todavía podemos introducir información incorrecta desde el punto de vista del negocio.

Por ejemplo:

* un precio negativo;
* una cantidad de stock inferior a cero;
* un descuento del 350 %;
* una fecha imposible según las reglas de la aplicación.

Aunque todos estos valores respeten el tipo de dato definido para la columna, representan información inválida.

Para evitar este tipo de situaciones utilizaremos la restricción ​**CHECK**​.

---

### ¿Qué es CHECK?

`CHECK` permite definir una condición lógica que todos los registros deben cumplir.

Cada vez que se inserta o modifica una fila, MySQL evalúa dicha condición.

Si el resultado es verdadero, la operación continúa.

Si el resultado es falso, la operación se cancela.

Podemos imaginar un `CHECK` como un filtro permanente instalado dentro de la propia tabla.

---

### Definiendo una restricción CHECK

Supongamos que ningún producto puede tener un precio negativo.

La definición sería:

```sql
CREATE TABLE Producto (

    IdProducto INT AUTO_INCREMENT PRIMARY KEY,

    Nombre VARCHAR(120) NOT NULL,

    Precio DECIMAL(10,2)
        CHECK (Precio >= 0)

);
```

En este caso cualquier valor inferior a cero será rechazado automáticamente.

---

### Otro ejemplo

También podemos controlar el stock.

```sql
Stock INT
CHECK (Stock >= 0)
```

De esta forma nunca existirán productos con cantidades negativas en el inventario.

Más adelante veremos que determinadas operaciones comerciales sí pueden disminuir el stock, pero el resultado final nunca podrá ser inferior a cero.

---

### Restricciones más complejas

La condición de un `CHECK` puede utilizar operadores lógicos.

Por ejemplo:

```sql
CHECK
(
    Descuento >= 0
    AND
    Descuento <= 100
)
```

Esto garantiza que el porcentaje de descuento permanezca siempre entre el 0 % y el 100 %.

---

### Compatibilidad con MySQL

Durante muchos años MySQL aceptaba la sintaxis de `CHECK` pero no la aplicaba realmente.

A partir de MySQL 8.0.16 la restricción comenzó a implementarse correctamente.

Por este motivo es importante trabajar con versiones modernas del servidor, como las utilizadas en este curso mediante Docker.

---

### Casos reales

En aplicaciones empresariales los `CHECK` suelen utilizarse para validar reglas sencillas.

Por ejemplo:

| Columna   | Restricción  |
| ----------- | --------------- |
| Precio    | >= 0          |
| Stock     | >= 0          |
| Descuento | Entre 0 y 100 |
| Edad      | >= 18         |

Las reglas de negocio más complejas suelen implementarse mediante procedimientos almacenados o en la lógica de la aplicación.

---

### Errores frecuentes

Uno de los errores más habituales consiste en intentar introducir dentro de un `CHECK` reglas excesivamente complejas.

Las restricciones deben utilizarse para validar condiciones simples y permanentes.

También es frecuente olvidar que algunas versiones antiguas de MySQL no aplicaban realmente estas comprobaciones.

### Ideas clave

* `CHECK` obliga a cumplir una condición lógica.
* Se evalúa automáticamente en cada inserción y modificación.
* Resulta ideal para validar precios, cantidades y porcentajes.
* Las reglas complejas deben implementarse mediante otros mecanismos.
* En este curso utilizaremos MySQL 8, donde `CHECK` funciona correctamente.

