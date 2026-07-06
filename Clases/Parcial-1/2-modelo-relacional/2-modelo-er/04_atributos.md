# Atributos

Las entidades nos indican **qué objetos existen** dentro del sistema.

Sin embargo, todavía desconocemos qué información almacenaremos sobre cada uno de ellos.

Por ejemplo, sabemos que existe la entidad ​**Cliente**​, pero ¿qué datos necesitamos guardar de cada cliente?

La respuesta la proporcionan los ​**atributos**​.

### ¿Qué es un atributo?

Un atributo es una característica que describe una entidad.

Cada atributo almacena un dato concreto sobre las instancias de esa entidad.

Por ejemplo, para la entidad **Cliente** podríamos almacenar:

* Nombre
* Apellidos
* Teléfono
* Correo electrónico
* Fecha de alta

Todos estos datos describen al cliente, por lo que son atributos.

### Un ejemplo sencillo

Supongamos la entidad ​**Producto**​.

Podría poseer los siguientes atributos:

```text
Producto

- Código
- Nombre
- Precio
- Stock
- Peso
```

Cada producto tendrá un valor distinto para cada atributo, pero todos compartirán la misma estructura.

### Clasificación de atributos

Existen distintas formas de clasificar los atributos.

Las más habituales son las siguientes.

| Tipo          | Descripción                                 |
| --------------- | ---------------------------------------------- |
| Simple        | No puede dividirse en partes más pequeñas. |
| Compuesto     | Puede descomponerse en varios atributos.     |
| Monovalorado  | Solo admite un valor por entidad.            |
| Multivalorado | Puede almacenar varios valores.              |
| Derivado      | Se obtiene a partir de otros atributos.      |

Aunque inicialmente utilizaremos atributos sencillos, es importante conocer esta clasificación.

### Atributos compuestos

Un atributo compuesto puede dividirse en otros más pequeños.

Por ejemplo:

```text
NombreCompleto

↓

Nombre

Apellido1

Apellido2
```

En bases de datos suele preferirse almacenar cada componente por separado, ya que facilita las búsquedas y las consultas.

### Atributos derivados

Algunos datos pueden calcularse a partir de otros.

Por ejemplo:

* Edad ← Fecha de nacimiento.
* Importe total ← Cantidad × Precio.
* Antigüedad ← Fecha actual − Fecha de contratación.

En muchos casos no es necesario almacenar estos valores porque pueden obtenerse automáticamente.

### Representación gráfica

En el modelo clásico de Chen, los atributos se representan mediante óvalos conectados a la entidad.

Como Mermaid no implementa completamente esta notación, durante el curso utilizaremos diagramas simplificados cuando sea necesario.

Lo importante será comprender el concepto, no memorizar la representación gráfica.

### Caso práctico

Para nuestra empresa comercial comenzaremos con algunos atributos básicos.

**Cliente**

* IdCliente
* Nombre
* Apellidos
* Teléfono
* Email

**Producto**

* IdProducto
* Nombre
* Precio
* Stock

Estos atributos se ampliarán conforme el negocio evolucione.

### Errores frecuentes

Entre los errores más habituales encontramos:

* Almacenar información calculable.
* Utilizar nombres ambiguos.
* Crear atributos con varios significados.
* Mezclar distintos datos en un mismo atributo.

Por ejemplo, un atributo denominado **DatosCliente** resulta demasiado genérico y debería dividirse en varios atributos independientes.

### Ideas clave

* Los atributos describen las características de una entidad.
* Cada entidad posee su propio conjunto de atributos.
* Existen atributos simples, compuestos, derivados y multivalorados.
* Conviene almacenar únicamente la información necesaria.
* Un buen diseño de atributos facilita las consultas y evita redundancias.

