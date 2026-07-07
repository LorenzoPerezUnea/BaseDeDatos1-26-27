# Atributos compuestos

Algunos atributos pueden dividirse en otros más pequeños con significado propio.

Estos reciben el nombre de ​**atributos compuestos**​.

Durante el diseño conceptual suelen representarse como un único atributo formado por varias partes.

Sin embargo, al transformarlos al Modelo Relacional normalmente se descomponen en columnas independientes.

### Un ejemplo

Supongamos que una entidad posee el siguiente atributo.

```text
Direccion
```

En realidad, una dirección está formada por varios componentes.

* Calle.
* Número.
* Piso.
* Código postal.
* Ciudad.
* Provincia.
* País.

Todos ellos poseen significado propio.

### Transformación

En lugar de almacenar un único texto, resulta preferible crear varias columnas.

```text
CLIENTE

----------------------------
Calle
Numero
Piso
CodigoPostal
Ciudad
Provincia
Pais
```

Ahora la información puede consultarse y filtrarse con mucha mayor facilidad.

### ¿Por qué dividirlo?

Imaginemos que la empresa desea responder a la siguiente consulta.

> Mostrar todos los clientes de Santander.

Si toda la dirección estuviera almacenada en un único campo de texto, la consulta sería mucho más complicada y menos eficiente.

Separando cada componente obtenemos una estructura mucho más útil.

### ¿Siempre deben dividirse?

No necesariamente.

Dependerá de las necesidades del negocio.

Por ejemplo:

```text
NombreCompleto
```

Podría dividirse en:

* Nombre.
* Primer apellido.
* Segundo apellido.

Si la empresa necesita buscar por apellidos o generar documentos oficiales, será recomendable almacenarlos por separado.

En cambio, si únicamente necesita mostrar el nombre completo, un único campo puede ser suficiente.

### Caso práctico

En nuestra empresa comercial utilizaremos atributos separados para la dirección de clientes y proveedores.

Esto permitirá realizar consultas geográficas, generar informes por ciudades y facilitar futuras integraciones con empresas de transporte.

### Ideas clave

* Un atributo compuesto puede dividirse en varios atributos simples.
* Durante la transformación suele convertirse en varias columnas.
* La decisión depende de las necesidades del negocio.
* Dividir correctamente los atributos facilita las consultas.
* Un buen diseño evita almacenar información compleja en un único campo de texto.

