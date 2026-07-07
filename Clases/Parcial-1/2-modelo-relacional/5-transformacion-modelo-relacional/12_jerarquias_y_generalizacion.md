# Jerarquías y generalización

Hasta este momento todas las entidades que hemos estudiado eran independientes entre sí.

Sin embargo, existen situaciones en las que varias entidades comparten gran parte de su información y únicamente se diferencian en algunos atributos específicos.

En estos casos resulta útil emplear una **jerarquía** o una ​**generalización**​.

El objetivo es evitar la duplicación de información y representar correctamente la relación de especialización entre distintas entidades.

### Un ejemplo sencillo

Supongamos que nuestra empresa trabaja con personas.

Todas ellas poseen:

* Nombre.
* Apellidos.
* Teléfono.
* Correo electrónico.

Sin embargo, algunas son clientes y otras empleados.

En el Modelo ER podríamos representarlo así.

```mermaid
erDiagram

PERSONA

CLIENTE

EMPLEADO
```

Conceptualmente, **Cliente** y **Empleado** son especializaciones de ​**Persona**​.

### El problema de la transformación

El Modelo Relacional no dispone de un mecanismo nativo para representar herencia.

Por ello debemos elegir una estrategia de diseño.

Existen tres enfoques principales.

### Estrategia 1. Una única tabla

Toda la información se almacena en una sola tabla.

```text
PERSONA

-------------------------------
IdPersona
Nombre
Telefono
Correo
TipoPersona
DescuentoCliente
SalarioEmpleado
Departamento
```

**Ventajas**

* Muy sencilla.
* Solo existe una tabla.

**Inconvenientes**

* Muchas columnas quedarán vacías.
* Mezcla información de distintos tipos de personas.

Esta estrategia suele utilizarse cuando las diferencias entre subtipos son pequeñas.

### Estrategia 2. Tabla padre y tablas hijas

Se crea una tabla para la información común y otra para cada especialización.

```text
PERSONA
----------------------
IdPersona
Nombre
Telefono
Correo

CLIENTE
----------------------
IdPersona
FechaAlta

EMPLEADO
----------------------
IdPersona
Salario
Departamento
```

Esta es la estrategia más utilizada en aplicaciones empresariales.

Evita duplicidades y mantiene el modelo organizado.

### Estrategia 3. Una tabla por subtipo

Cada subtipo almacena toda su información.

```text
CLIENTE

IdCliente
Nombre
Telefono
Correo
FechaAlta

EMPLEADO

IdEmpleado
Nombre
Telefono
Correo
Salario
Departamento
```

Aunque es sencilla de entender, duplica información y dificulta el mantenimiento.

Solo suele utilizarse cuando los subtipos son prácticamente independientes.

### ¿Cuál utilizaremos?

En nuestro caso de estudio todas las entidades representan conceptos claramente distintos.

Por ello ​**no utilizaremos jerarquías durante las primeras fases del curso**​.

Sin embargo, conocer estas estrategias resulta importante porque aparecen con frecuencia en aplicaciones de gran tamaño como sistemas hospitalarios, universitarios o de recursos humanos.

### Ideas clave

* Las jerarquías representan relaciones de especialización.
* El Modelo Relacional no implementa herencia de forma directa.
* Existen tres estrategias principales para representarla.
* La estrategia "tabla padre + tablas hijas" suele ser la más flexible.
* La elección depende de los requisitos del proyecto y del volumen de datos.

